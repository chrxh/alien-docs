# Simple swarmbot

#### Abstract

Cells in ALIEN can perform a wide variety of actions. We will address cell programs, mass sensors and motion control in this section. These functions will be explained by building a simple swarm robot that scans its environment for particle concentrations with a specific color and moves in that direction.

## Cell skeleton

The basic idea is that our swarmbot scans its environment for certain particle concentrations and as soon as it finds something, it heads for the target. If the target is on the left side, a forward movement combined with a left turn should take place and in the other case a right turn.

A simple skeleton for our purpose consists of a loop-shaped structure in which a token can circulate. In this structure, we need a _muscle_ on both sides that provides us with an impulse depending on the direction we want to direct. We also need to accommodate a sensor that will give us the distance and angle where particle concentrations of a certain color are located.

![Cell skeleton of a simple swarmbot](../../.gitbook/assets/skeleton.svg)

The above structure is composed of 7 cells and consists of 3 functional units:

* The 2 cells on the left side are used to generate an impulse to steer to the right. One of these cells is a computational cell and is used to control the muscle cells. A muscle cell can only generate an impulse in the direction or opposite direction from which the token originates.
* We still need a similar unit on the right side. A forward impulse on the right side leads to a left steering of the total structure.
* In front of the swarmbot is our visual unit. It consists of a computational cell and a mass sensor.

We now construct the basic structure in the editor by creating 7 cells and connecting them individually. Because there are only 6 different token branch numbers, it is not possible to reproduce a directed cycle. Here we will help later with a special cell program. Furthermore, we create a token at an arbitrary cell. To this end, we inspect one of these cells in the pattern editor (shortcut ALT+N) and click on the tab with the plus symbol.

![Skeleton of our swarmbot in ALIEN](../../.gitbook/assets/skeleton.PNG)

We set the cell specializations (_Computation_, _Muscle_ and _Sensor_) as indicated in the screenshot above. The different cell types will be explained in more detail in the following sections and then an  appropriate implementation for our machine will be presented.

## Working principle of a computing cell

A computing cell has two memories: One memory in which instructions are encoded and a data memory. As soon as a token enters such a cell, its instructions are executed. The instructions have access to the data memory of the cell as well as to the data memory of the token. Basically, a cell program can consist of a maximum of 15 instructions. Each instruction is represented as 3 bytes in the memory. The data memory of a cell contains 8 bytes while the memory of a token contains 256 bytes. ALIEN provides a built-in compiler that allows the user to write the code in an assembler-like language. The following instructions are supported:

```
    mov op1, op2
    add op1, op2
    sub op1, op2
    mul op1, op2  
    div op1, op2  
    xor op1, op2  
    or op1, op2  
    and op1, op2 
    if op1 > op2
    if op1 >= op2
    if op1 = op2  
    if op1 != op2
    if op1 <= op2
    if op1 < op2
    else
    endif
```

In C syntax, for example, the statement at line 1 would read as `op1 = op2;` and at line 2 `op1 += op2;`. `op1` should point to a particular byte in memory, while `op2` can be a memory byte or a constant (8 bits size). There are several ways to reference a memory byte for `op1` or `op2`:

* Direct reference to a token memory byte: In this case a byte in the token memory is referenced via an 8 bit address. The address can be specified as decimal or hexadecimal value. Syntax (example): ** `[32]` or `[0x20]`**
* Direct reference to a cell memory byte: A memory byte of the cell can also be referenced. Syntax (example): ** `(0)`**
* Indirect reference to a token memory byte: It is also possible to obtain the address itself from memory when referencing a token memory byte. Syntax (example): **`[[32]]` or `[[0x20]]`** In this case the actual address is obtained from `[0x20]` and then used to reference the corresponding memory byte.

To make writing code easier, there is a symbol table where one can specify aliases for constants and references to memory bytes. For instance, a code like

```
if i=0
  mov CONSTR_IN_OPTION, CONSTR_IN_OPTION::STANDARD
  mov CONSTR_INOUT_ANGLE, 0xD0
endif
if SCANNER_OUT = SCANNER_OUT::FINISHED
  mov CONSTR_IN_OPTION, CONSTR_IN_OPTION::FINISH_WITH_DUP_TOKEN_SEP
endif
mov CONSTR_IN_CELL_MAX_CONNECTIONS, CONSTR_IN_CELL_MAX_CONNECTIONS::AUTO
mov CONSTR_IN_DIST, 0x78
mov CONSTR_IN_UNIFORM_DIST, CONSTR_IN_UNIFORM_DIST::YES
```

is much easier to understand than the decompiled machine code

```
if [0xff] = 0x0
  mov [0x7], 0x0
  mov [0xf], 0xd0
endif
if [0x5] = 0x1
  mov [0x7], 0x6
endif
mov [0x11], 0x0
mov [0x10], 0x78
mov [0xd], 0x1
```

The symbols can be viewed in the _Symbols_ window reachable via the _Editor_ menu. Some of the memory bytes are used to control other cell functions. There are many predefined symbols for this purpose.

## Working principle of a muscle cell

Muscle cells can perform four different operations. The reference distance of the muscle cell to the predecessor cell is changed and, if necessary, an impulse is generated at the same time. The predecessor cell designates the cell from which the token originates that has just entered the muscle cell.

![The four different operations of a muscle cell](../../.gitbook/assets/muscle.svg)

The graphic above illustrates the different operations. Here we have two connected cells (a computation cell on the left and a muscle cell on the right) and a token that jumps from the left to the right cell and thus triggers the muscle function.

* The first operation refers to a pure contraction. Here, the reference distance of the cell connections is reduced by a fixed factor. This results in a force that brings the cells closer together.
* In the second case, the reference distance is also reduced and at the same time the muscle cell is given a forward momentum.
* The third operation describes a pure expansion. The distance between the connected cells is increased.
* Analogous to the second case, the fourth operation leads to an increase in distance and, at the same time, to a backward momentum of the muscle cell.

The indication of which operation should be performed is specified in the token memory. To simplify programming, there are default symbols for the memory location and its values. These can be viewed in the symbol editor, which can be opened in the editor menu.

![Symbol editor](../../.gitbook/assets/symbols.PNG)

The symbol `MUSCLE_IN` __ denotes the memory byte in the token where the muscle cell reads the operation to be performed. It is an alias for the memory byte at position 36, which can also be written as \[36] in the code. The different operations, on the other hand, are encoded via the symbols `MUSCLE_IN::CONTRACT_RELAX`, `MUSCLE_IN::CONTRACT`, `MUSCLE_IN::EXPAND_RELAX`, `MUSCLE_IN::EXPAND` in the above order. These simply refer to constant values.

For example, if we want the muscle cell to perform a contraction, we must set the appropriate value in the token memory beforehand. There the following command in a preceding computation cell we do.

```
mov MUSCLE_IN, MUSCLE_IN::CONTRACT_RELAX
```

## Working principle of a sensor cell

A cell with a sensor is able to detect particle concentrations with a certain minimum density and a certain color in the vicinity. It will return the relative distance and relative angle of the found target. If there are multiple targets, the one with the smallest distance is considered. Let us illustrate its working with a simple example.

![Illustration of the operation of a sensor](../../.gitbook/assets/sensor.svg)

To understand the functionality, we consider the cell of the sensor and the predecessor cell of the token. In the graphic above we see in the center a sensor cell to which a token jumps from a cell connected on the left. From the relative position of both cells we can define what means _front_ and _back_. In the case above, e.g., the direction to the right (sensor line) is specified as the front.

We now assume that we want to search for nearby green particle accumulations. In our illustration, three colored clusters can be seen. The cluster with the smallest distance is yellow and then two green ones follow. Our sensor would detect the middle one and would measure the relative distance _d_ and the relative angle _α_ from that cluster. The sign of the angle gives us the information whether the target is above or below the sensor line. Since the determined target in our case is below the sensor line (red shaded area), the angle is positive.

## Implementation of a muscle control

In the following we will focus on the concrete implementation. To control the muscles for our swarmbot, we need the following cell programs:

![Cell programs for the muscle control](<../../.gitbook/assets/muscle programming.PNG>)

Let us have a closer look at the cell program on the right side first:

```
mov j, SENSOR_OUT
add SENSOR_INOUT_ANGLE, 64
mov MUSCLE_IN, MUSCLE_IN::DO_NOTHING
if i=1
  mov MUSCLE_IN, MUSCLE_IN::CONTRACT_RELAX
  mov i, 0
else
  if i=0
    if j=SENSOR_OUT::CLUSTER_FOUND
      if SENSOR_INOUT_ANGLE>128
        mov MUSCLE_IN, MUSCLE_IN::EXPAND
        mov i, 1
      endif
    endif
  endif
```

* Line 1: The memory byte which contains the return value from the sensor is stored in another memory byte with the symbol `j`. This is necessary because different cell functions sometimes use the same memory byte as output.
* Line 2: An angle correction of sensor data is performed here. We will examine this in more detail in the next section.
* Line 3: As default, we instruct the muscle cell to do nothing. This will always be the case when the sensor finds nothing.
* Line 8 - 15: It is checked whether the memory byte `i` is equal to `0`. This is the case if no muscle operations were performed in the last cycle. It is then checked whether the sensor has found something and whether the target is on the left side (with respect to the orientation in the picture above). The muscle cell on the right hand side is instructed to perform an expansion together with a backward momentum, which will cause the swarmbot to turn left. The memory byte `i` is set to `1` to perform a contraction in the next cycle.
* Line 4 - 7: The memory byte `i` is equal to `1` if an expansion was instructed in the last cycle. In order for the cell connection to regain its original reference distance, a contraction without an additional momentum is now instructed.

{% hint style="info" %}
In the code one can see that an `endif` is missing. It can be omitted at the end of a program. This is even necessary here, because a cell program can only consist of a maximum of 15 commands.
{% endhint %}

The program of the computation cell on the left side works analogously with the difference that here a forward momentum must be generated to initiate a clockwise rotation. This is due to the fact that the token reaches the muscle cell from below while in the right side it reaches the muscle cell from above (i.e. the frame of reference is rotated by 180°).

```
mov BRANCH_NUMBER, 3
mov MUSCLE_IN, MUSCLE_IN::DO_NOTHING
if i=2
  mov MUSCLE_IN, MUSCLE_IN::EXPAND_RELAX
  mov i, 0
else
  if i=0
    if j=SENSOR_OUT::CLUSTER_FOUND
      if SENSOR_INOUT_ANGLE<128
       mov MUSCLE_IN, MUSCLE_IN::CONTRACT
        mov i, 2
      endif
    endif
  endif
endif
```

* Line 1: Here a new branch number is assigned to the token. Normally the token obtains the branch number of the underlying cell. However, in our case we want the token to jump from the cell with the number 4 to the cell above with the same number. Since tokens always jump to the cells with the next higher number, we have to set the branch number of the token to 3.
* Line 2 - 15: The code works similarly to the previous one with the difference that we first perform a contraction and then an expansion. Since this results in a right turn, this operation is only performed when the sensor has found a target on the right side.

Our machine would not work properly yet. For this we still need to adjust the sensor appropriately.

## Implementation of a sensor control

The control of a sensor is relatively simple compared to the muscle cells. We only need to set a few options that provide the needed information for the sensor. For this purpose we can place the following small program in the upper left computation cell for our swarmbot.

![Cell programs for sensor and muscle control](<../../.gitbook/assets/sensor programming.PNG>)

The code reads as:

```
mov SENSOR_IN, SENSOR_IN::SEARCH_VICINITY
mov SENSOR_IN_MIN_DENSITY, 5
mov SENSOR_IN_COLOR, 1
```

The code is actually self-explanatory. A sensor knows two different working modes, which are defined in the memory byte `SENSOR_IN`:

* The scanning of the entire vicinity, which is indicated by the value `SENSOR_IN::SEARCH_VICINITY`.
* Scanning of a certain direction for which it is necessary to set the value `SENSOR_IN::SEARCH_BY_ANGLE`.

In line 2 we specify the sensitivity of the sensor. The memory byte SENSOR\_IN\_MIN\_DENSITY contains the minimum mass density of particle accumulations that the sensor would detect as potential targets. The density value indicates the number of particles in an area with size 8 x 8.

Finally, we provide a particle color in line 3. A value between 0 to 6 is expected here. The value 1 corresponds to the red color.

When the sensor function has been executed, we can retrieve the result in `SENSOR_OUT` whether a target has been found or not. If this is the case, it has the value `SENSOR_OUT::CLUSTER_FOUND` (see code from the muscle control). We obtain the angle of the target in `SENSOR_INOUT_ANGLE`, the distance in `SENSOR_OUT_DISTANCE` and the exact density in `SENSOR_OUT_MASS`. It should be noted that all these information are encoded in one byte each. For the specification of the angle, 0° to +180° correspond to the byte values from 0 to 127 and -180° to 0° correspond to the byte values from 128 to 255.

The instruction

```
add SENSOR_INOUT_ANGLE, 64
```

taken from the code of the computation cell on the right side calculates the relative angle of our target if we would rotate our frame of reference by 90° counterclockwise. It corresponds to the reference frame where the muscle cells are controlled.

Also the line

```
if SENSOR_INOUT_ANGLE < 128
```

which is used in one of the computational cells for the muscle control becomes now clear: We just check whether the angle is positive or negative.

## Test the result

We have now finished putting together our machine. One can also find it as a pattern file at `./examples/patterns/swarmbots/Interceptor (Red Target).sim` if something does not work as expected. To experiment with our creature, we can, for example, build a large red rectangular cluster of cells nearby. We should then observe how the red cluster is pursued or orbited by the swarmbot while running the simulation (with a slow down!)

![Swarmbot orbiting a red cell cluster](<../../.gitbook/assets/swarmbot orbit.PNG>)
