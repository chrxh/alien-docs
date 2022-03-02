# First steps with the editor

#### Abstract

In this section we will familiarize ourselves with some basic functions of the editor. The user has the possibility to directly intervene both in running and paused simulation. In the latter case, extensive editing features are available, a few of which will be mentioned here.

### Apply forces to objects in a running simulation

For testing purposes we load the simulation `./examples/simulations/physics/Sand Stones.sim`. In this simulation, we can try out pushing simple geometric objects around with the mouse cursor. We first zoom out a bit and switch from the navigation mode to the editor by clicking on the pencil icon at the bottom left (or alternatively via the _Editor_ menu and then by invoking _Activate_).

![Initial configuration of Sand Stones.sim](<../.gitbook/assets/sand stones.png>)

As soon as we have clicked on the play button, the simulation runs and we can exert force on the objects by holding down the left mouse button. The faster we move the mouse, the stronger the acting forces are.

### Select und move objects

After the simulation is paused, we can select objects and move them around by dragging and dropping with the left mouse button. Selected objects are generally highlighted with a higher brightness. If one wishes to extend the selection to several objects, one can accomplish this by holding down the CTRL key. It is also possible to select a whole area by dragging a rectangular box with the right mouse button pressed.

![Rectangular selection area](<../.gitbook/assets/rectangular selection.png>)

The Selection info window shows how many entities have been selected. A selection always consists of two levels: On the one hand the directly selected entities (cells and energy particles) and on the other hand the extended selection, which additionally contains the connected cells.

When a selection is shifted with the mouse, the extended selection is actually affected by default. This behavior can be changed with the toggle _Rollout to cell clusters_. If it is turned off, only the immediate selection is affected by the editing actions. The toggle can also be switched off temporarily by holding down the SHIFT key. As one may notice after some experimentation, the cell clusters can be rewired when the switch is disabled. More precisely:

* If one moves a cell too far from its connected cell, the connection will be removed.
* If one brings a cell in the proximity of another cell and if both cells are capable of making connections, a new connection will be established.

![Rewire cell clusters](../.gitbook/assets/rewiring.png)

### Reference versus actual configuration
