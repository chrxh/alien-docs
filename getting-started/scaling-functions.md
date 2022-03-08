# Scaling functions

#### Abstract

We will continue in this article by exploring ways to scale simulation data. One powerful method that we have already encountered is the mass copy of patterns from a template. This time, we will be dealing with a pre-built machine and using it to create a large formation on a grid layout. In doing so, we can influence the velocities and the angle of the individual specimens. And to make the whole thing a bit fun, we construct a world in which countless interceptor machines chase after a large object. In the end, we'll add one more on top and duplicate the entire world.

## Initial world design

The basic design is as follows: We place a larger cell cluster, such as a ring in the center of the world. Then we load an existing pattern, which is a machine that regularly scans its environment with the help of a sensor cell. It looks for mass concentrations with a certain color. When the sensor cell finds something, the muscle cells are triggered to direct the machine to move toward the mass. It also attacks its target with the help of digestive cells.

We start by creating an empty world with dimensions of 1000 x 1000 units and make some adjustments to the simulation parameters:

* Friction is set to 0.001 (default)
* Radiation strength is set to 0
* Cell specialization: Sensor function -> Range is set to 350 units

With the last parameter we set the range of the sensor cells. Then we switch to the editor and create a blue ring with an outer radius of 30 and an inner radius of 25. With the pattern editor we load the file `./examples/patterns/swarmbots/Attacker (Blue Target).sim` into our world and place it below the ring.

![Blue ring with a swarmbot](<../.gitbook/assets/interceptor world design.png>)

The tiny swarmbot is colored red and searches, navigates and attacks cell clusters with a blue color. The orientation of the swarmbot is important because it cannot move backwards: The upper part is the front and the lower the back part. Threshold values for the desired mass density can be set dynamically by the machine. .

{% hint style="info" %}
To reprogram the swarmbots behavior, a deeper knowledge of cell programming is required, which we will discuss in a later article
{% endhint %}

We can run the simulation for testing (important: take a snapshot and enable slow down). One can see nicely that the swarmbot heads for the blue ring, bounces off due to the collision and takes a new course again. After some time it is on a circular course around the ring. When the friction is altered, the behavior changes somewhat.

## Mass copy function on grid layout

A simulation with only one swarmbot is actually relatively boring, because it cannot do much damage to the ring. It would be much more exciting to have thousands of attacking specimens at the same time. As the workload is also distributed to thousands of GPU threads, this should not be a problem for our graphics card.

The multiplier window allows us to create a formation of swarmbots arranged in a grid. It is important that we have selected the already existing one. Then we open the multiplier window and click on the first toolbar button. For the moment we are modest and create copies on a 100 x 30 grid with 6 units between each copy horizontally and vertically. After we click _Build_, the copies are created and selected automatically. In this state it is possible to undo this action by invoking the _Undo_ button, in case we want to change something in the settings.

![Copies of the swarmbot](<../.gitbook/assets/swarmbot copies.png>)

{% hint style="info" %}
The simulation code on the GPU works with arrays of fixed size for all entities. The array limits can be quickly exceeded after scaling the data. Fortunately, there is an automatic adjustment that enlarges the arrays as needed. The _Log_ window reports such events.
{% endhint %}

When one now starts the simulation, one observes a much more dynamic world. The ring is almost completely destroyed after a short time.

It is also still worth trying to set a slight vertical velocity increment. For example, in the _Multiplier_ panel we can set the _Velocity Y increment_ to 0.02 in the part for the vertical settings. Have fun trying it out!

## Scaling up entire worlds

With the previous shown scaling functions, we can multiply a pattern arbitrarily in a given world. But now we want to go one step further: We want to scale up not only the patterns but the complete space!

This function is very useful, for example, to produce a significantly larger population from a small one at a later time during an evolution simulation (and, of course, it also works the other way around).
