# Particle editing

#### Abstract

It is possible to select any entity, manipulate their properties and memory, and get real-time updates during a running simulation. For this purpose, editing windows can be pinned to particles. We will make use of this feature by inspecting a self-replicating particle machine in more detail and perform specific changes.

## Pin editing windows to cells

For testing purposes we load the simulation file `./examples/simulations/evolution/Loops Evolved.sim`. It contains only one self-replicating cell cluster in the center and otherwise only passive structures that serve as food source. The self-replicating structure has a loop shape, can  move randomly, eat other particles to obtain energy from its environment and copy itself by inspecting its own structure to rebuild it. Can you find the little particle machine right away?

![](../.gitbook/assets/loop.png)

Our first goal is first to inspect the internals of the loop in more detail. We zoom in, activate the editor together with the information overlay, select the entire loop and click the tool button with the microscope in the _Pattern editor_ (or even faster: ALT + N). For each selected particle, a window is now pinned, which displays all internal properties and offers editing. We place the windows so that we can easily see the cells. In addition, the overlay information allows us to identify the so-called token branch numbers and cell specializations.

The cell that glows white possesses a token. By default tokens always jump in the next time step to the cells with the next higher token branch number with respect to a modulo arithmetic. But it is possible to bypass this mechanism and let the token jump to another cells. This trick is also used here and necessary, because the loop consists of 8 cells and we only have 6 different token branch numbers. We will discuss this in more detail in a later article.

![](<../.gitbook/assets/particle editors.png>)

## Autotracking and live updates&#x20;



## Change cell properties
