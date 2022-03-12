# Particle editing

#### Abstract

It is possible to select any entity, manipulate their properties and memory, and get real-time updates during a running simulation. For this purpose, editing windows can be pinned to particles. We will make use of this feature by inspecting a structure building particle machine in more detail and perform specific changes.

## Pin editing windows to cells

We create a new simulation with the dimensions 1000 x 1000 and set the radiation strength and rigidity value to 0. Then, we open the pattern editor and load the example `/examples/patterns/builders/Spiral Builder.sim` into our world.

Our first goal is first to inspect the internals of the builder more detail. We zoom in, activate the  information overlay, select all cells of the cell cluster and click the tool button with the microscope icon in the _Pattern editor_ (or even faster: ALT + N). For each selected particle, a window is now pinned, which displays all internal properties and offers editing. We place the windows so that we can easily see the cells. In addition, the overlay information allows us to identify the so-called token branch numbers and cell specializations.

The cell that glows white possesses a token. By default, tokens always jump in the next time step to connected cells with the next higher token branch number with respect to a modulo arithmetic. But it is possible to bypass this mechanism and let the token jump to another cells. This trick is also used here and necessary, because the builder consists only of 5 cells and we have 6 different token branch numbers. We will discuss this in more detail in a later article.

![Inspecting a machine which build spiral structures](<../.gitbook/assets/particle editors.png>)



## Autotracking and live updates&#x20;



## Change cell properties
