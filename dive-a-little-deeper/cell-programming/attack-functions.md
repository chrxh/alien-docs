---
description: >-
  Warning: This documentation is out of date and does not describe the behavior
  of the current version 4.0.
---

# Attack functions

#### Abstract

In ALIEN, a cell digestion process refers to the attempt of converting a foreign cell into usable energy and can also be considered as a form of attack. This capability to extract energy is required by cell clusters to have a functioning metabolism. To explain its functioning and implementation, the swarmbot from the previous article will be upgraded and equipped with an attack function.

## Cell skeleton

Let us adopt the swarmbot from the last article and modify it to our purposes. The basic structure does not need to be changed, but we will adjust the cell functions and the control logic a bit. First of all, we need to accommodate a digestion unit. The front side of the machine is ideal for this because it will be in contact with other cells most frequently. In our case, it will look like this.

![Cell skeleton of a swarmbot with attack capabilities](<../../.gitbook/assets/skeleton attacker.svg>)

As one can see, we have to sacrifice a computational cell for this purpose. However, we still have a cell available at the bottom center, which we had not used so far. Before we get to the implementation details, let us give a more detailed explanation of the digestion process.

## Working principle of a digestion cell

The basic principle is simple: As soon as a digestion cell is triggered by a token, it searches for cells in the immediate vicinity that are not connected to it directly or via another cell. For each of these matched cells, it is calculated how much internal energy can be drawn from it. However, the amount of energy to be extracted depends strongly on the simulation parameters and on the input from the token memory. In the worst case, the digestion cell even loses energy if the foreign cells do not meet certain criteria. Let us discuss the corresponding simulation parameters grouped under _Cell specialization: Digestion function_:

#### Energy cost

If we set the energy cost greater than 0, then after each activation of the digestion cell, even if no nearby cells were found, the internal energy is decreased to an amount specified by this parameter and in return released as an energy particle to the environment. Thus, a large value penalizes structures that attack their vicinity on a massive and unselective basis.

#### Target color mismatch penalty

This parameter (among others) assigns a special meaning to the color of a cell. One can also think of the cell color as another form of specialization, which can contribute to more diverse ecosystems. In the token memory, a specific color can be set for the cells that are aimed to be digested. This effect will be activated if the _Target color mismatch penalty_ parameter is greater than 0. If the color of the cell to be digested does not match the specified color, less energy is drawn from it, depending on the value of this parameter. In the extreme case, when the parameter is greater than 1, the cell even loses energy when it tries to digest cells with the wrong color.

#### Successive color dominance

This parameter controls the influence of the color combination of the digestion cell and the cell being digested on the energy extraction. Each color can be assigned a numerical value between 0 and 6. We say that a color `a` is the successor of another color `b` if the cyclic condition `a ≡ b + 1 (mod 7)` holds true.&#x20;

![Visualization of the cyclic condition. Right: dominant cell color, Left: inferior cell color](<../../.gitbook/assets/color dominance.svg>)

If the _Successive color dominance_ parameter is greater than 0 and the cyclic color condition is not met (i.e., the digestion cell does not have the dominant color with respect to the digested cell), then less energy can be extracted.

#### Geometry penalty

This parameter can be used to regulate the extent to which digestion processes extract less energy when the local geometry of the digestion cell does not match with that of the digested cell. For this purpose, two angles are calculated as illustrated in the figure below. We say here that the local geometries of both cells deviate when the sum of the angles α and _β_ differs from 360°. The stronger the deviation is and the larger the _Geometry penalty_ parameter is chosen, the less energy can be extracted in the digestion process.

![Left: digestion cell, Right: cell to be digested](<../../.gitbook/assets/geometry penalty.svg>)

Below is an example for a perfect match (i.e., α + _β_ = 360°). In this case, the maximum energy can be obtained from the process.

![Perfect match with no geometry penalty](<../../.gitbook/assets/geometry match.svg>)

#### Connection mismatch penalty

The idea behind this parameter is that it should be more difficult to decompose a cell with many cell connections than one with fewer ones. More specifically, the number of connections of the attacking cell is compared to that of the attacked cell. If this parameter is greater than 0 and the attacked cell has more connections than the attacking cell, less energy is obtained in the digestion process. With a large value of this parameter, cell can better protect itself from attacks provided they have more connections. With a value of 1, a cell can no longer be digested if the attacking cell has fewer connections.

#### Token penalty

A positive value causes a cell to be harder to digest (= less energy can be obtained through the digestion process) if it has tokens. With a value of 1, a cell can no longer be digested if there are tokens on it.

## Implementation

We do not have to change too much in the programming of our swarmbot. First of all, we move the code to control the sensor down into the computing cell. Secondly, we select _Digestion_ as the specialization in the upper left cell. The result should look something like this.

![Our extended swarmbot with attacking capabilities](<../../.gitbook/assets/swarmbot upgraded.PNG>)

If the _Target color mismatch penalty_ parameter is greater than 0, the digestion cell reads a target color from token memory to perform its process. This information is given in the token memory byte referenced by the symbol `DIGESTION_IN_COLOR`. However, the symbol references the same memory location as `SENSOR_IN_COLOR`. This means that the color of the cells that the sensor should detect represent the target color for the digestion process.

The result of the cell process is returned to `DIGESTION_OUT` and can take one of the following values:

* `DIGESTION_OUT::NO_TARGET`: There were no foreign cells in the direct vicinity.
* `DIGESTION_OUT::SUCCESS`: There was at least one cell in the vicinity. Each of these cells have been tried to digest and none of them was poisoned (see next point).
* `DIGESTION_OUT::POISONED`:  There was at least one cell in the vicinity which was poisoned. Poisoned cells can only occur if the _Target color mismatch penalty_ parameter is greater than 1.

## Testing the result

An interesting way to try out our upgraded swarmbot is to create two grid formations of swarmbots via the _Multiplier_ window: The first formation consists of blue machines we have just created. The second formation in close proximity consists of red machines, where we will change the control code for the sensor in order to detect blue cells. Specifically, we set

```
mov SENSOR_IN_COLOR, 0
```

in the computing cell in the lower part. In effect, we have created two swarms that chase and attack each other.

![Two swarms chasing each other](<../../.gitbook/assets/swarmbot fighting.PNG>)
