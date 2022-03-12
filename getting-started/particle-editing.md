# Particle editing

#### Abstract

It is possible to select any entity, manipulate their properties and memory, and get real-time updates during a running simulation. For this purpose, editing windows can be pinned to particles. We will make use of this feature by inspecting a structure building particle machine in more detail and perform specific changes.

## Pin editing windows to cells

We create a new simulation with the dimensions 1000 x 1000 and set the radiation strength and rigidity value to 0. Then, we open the pattern editor and load the example `/examples/patterns/builders/Spiral Builder.sim` into our world.

Our first goal is first to inspect the internals of the builder more detail. We zoom in, activate the  information overlay, select all cells of the cell cluster and click the tool button with the microscope icon in the _Pattern editor_ (or even faster: ALT + N). For each selected particle, a window is now pinned, which displays all internal properties and offers editing. We place the windows so that we can easily see the cells. In addition, the overlay information allows us to identify the so-called token branch numbers and cell specializations.

The cell that glows white possesses a token. By default, tokens always jump in the next time step to connected cells with the next higher token branch number with respect to a modulo arithmetic. But it is possible to bypass this mechanism and let the token jump to another cells. This trick is also used here and necessary, because the builder consists only of 5 cells and we have 6 different token branch numbers. We will discuss this in more detail in a later article.

![Inspecting a machine which build spiral structures](<../.gitbook/assets/particle editors.png>)

The pinned windows are identical in structure and consist of several tabs:

* _General_: Contains the properties common to each cell. Among other things, we can change the cell specialization here. In this example, we only use _Computation_ and _Construction_ functions. If the specialization is changed, the tabs may also change.
* _Code_: This tab is only displayed for computation cells. It contains the source code that the cell executes when a token passes it. The code is written in an assembler-like language and  consist of a maximum of 15 operations. It is translated into a machine language for the cells. If the source code is edited, it is immediately compiled and a feedback from the compiler is given under _Compilation result_.

{% hint style="info" %}
Inside the code tab next to the compilation result there is a tooltip that gives an overview of the assembly language.
{% endhint %}

* _Memory_: This tab is also only visible for computation cells. Here one can view and edit the memory contents of the cell with a hex editor. Each computation cell has 2 different memories: a fixed and a variable memory. The fixed memory is called instruction section and contains the translated source code. Each instruction is compiled into 3 bytes. The variable memory is called Data section and is the memory that can be accessed by the program itself.
* _In/out channels_: This tab is visible for all non-computation cells and only gives general information about the input and output signals that are accessed from the token memory.
* _Token \[1|2|3|...]_: Cells can hold a certain number of tokens. Each token is displayed in an extra tab. In each tab the energy value and the memory of the corresponding token can be edited. The cell code of computation cells can also access this memory.

## Autotracking and live updates&#x20;



## Change cell properties
