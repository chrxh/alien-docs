# Evolution experiments

#### Abstract

We will perform evolutionary simulations by injecting self-replicating machines into pristine worlds. Mutations will lead to gradual optimizations of the individuals. In this context, we want discuss the influence of crucial simulation parameters on cell functions. ALIEN offers advanced features like inhomogeneous parameter values, which we will also make use of. We will then address how larger self-replicating machines can be made functioning.

## Simple simulation setup for small self-replicators

The basic idea is simple: We create an empty world, fill it with enough particles serving as food source, inject a self-replicating machine and activate occasional mutations. The rest is done by the ongoing simulation.

We can already load a simple setup using the simulation file `./examples/simulations/evolution/Loops.sim`. Or to reconstruct it, we create a new simulation with the size 1000 x 500, fill it with enough particles (80,000 should be sufficient) and load the pattern `./examples/patterns/replicators/Loop.sim` into it. The self-replicating structure has a loop shape, can move randomly, eat other particles to obtain energy from its environment and copy itself by inspecting its own structure to rebuild it. Can you find the little particle machine right away?

![Initial setup](../.gitbook/assets/loop.png)

Let us take a closer look at the loop and inspect its computation cells:

![Close up of the loop](<../.gitbook/assets/loop closeup.png>)

The cell cluster consists of 2 muscle cells for movement, a scanner cell for reading out the internal structure, a digestion cell for transforming surrounding particles into internal energy, a construction cell for creating new particles and several computational cells that are used for coordination. The exact replication process will be discussed in a later article. The cell code is also shown in the inspected cells.

In our first experiment we use almost the default settings for the simulation parameters except for:

* _Radiation strength_: 0
* _Cell mutation rate_: 0.0000016
* _Token mutation rate_: 0.0005

The cell mutation rate indicates the probability with which a byte of the cell memory or other properties (e.g. specialization, color, etc.) are randomly changed per time step. The analog setting is also available for the tokens.

If we now run the simulation for a few minutes, our world already does not look that idyllic anymore. The replicators have then eaten up most of the free resources and are now increasingly competing with each others.

![Loop replicators after some minutes](<../.gitbook/assets/loop later.png>)

If you let the simulation run even longer, mutations are increasingly created that multiply faster or move differently. The color also changes more or less randomly. An example of a longer simulation run can be found in the file `./examples/simulations/evolution/Loops Evolved.sim`.

{% hint style="info" %}
One way to increase the simulation speed is to disable _Render simulation_ in the _View_ menu.
{% endhint %}

After some time one can experiment with the simulation parameters. For example, we can increase the mutation rates, or make the world more hostile to life by increasing the radiation. If one does not overdo it, the population should be able to adapt. A good possibility for the control offers the statistics window which can be activated in the _Window_ menu. It shows the total number of tokens in the world, which in turn is a measure of the cell activities. If this value falls too fast, then there is a danger that the population will die out.

## Simulations with larger self-replicators

In our last example, we initially started with replicators of nearly minimal size, although even smaller structures with certain functional trade-offs are conceivable. Somewhat more exciting and challenging are experiments with self-replicating machines, which are larger and consist of a more complex particle network. The copying process will take longer and we have to replicate particles with more connections. Furthermore, the sensitivity with respect to the simulation parameters requires a precise tuning. A significant advantage, however, is that larger structures can accommodate more functionality and that the optimization potential in evolutionary simulations is generally greater.

As in the previous section, we can build our own world and inject a large replicator. The pattern `./examples/patterns/replicators/Hexogon.sim` is available for this purpose. There are a few things to keep in mind here:

* One must be careful to distribute the food properly, because this machine needs longer for movement maneuvers. It is a good idea to place many small square cell clusters.
* One should also have several copies of the hexagon ready at the beginning because unfortunate coincidences can damage some.
* Larger cell clusters are significantly more susceptible to mutations. We should set the mutation rates very low at the beginning. For instance, a cell mutation rate of 0.000001 and a token mutation rate of 0.0001 should work.

There is also a readymade simulation for it, where all parameters are tuned and the food sources are distributed: `./examples/simulations/evolution/Hexagons.sim`

![Internals of the hexagon replicator](<../.gitbook/assets/hexagon closeup.png>)

In contrast to the loop replicator, this one also has a sensor cell. This machine uses it to locate food sources and to control its muscle cells such that it moves there. However, due to its size, this navigation takes a very long time.&#x20;

Once we have assembled or loaded our world, we can start the simulation. As it can be noticed, we have to run the simulation much longer to have all the free food sources used up and to have the world filled with replicators. However, if we wait sufficiently long, we notice that at some point mutations arise that can multiply much more efficiently.

Have fun watching it!

![The hexagon world after more than 10 million time steps.](<../.gitbook/assets/hexagons evolved.png>)

## Color semantics for cell types

It can be observed that after some time a certain equilibrium develops. The population size remains roughly stable, gradually fewer traits are changing and evolutionary leaps become rarer. One way of regularly breaking through equilibria and creating more refuge areas is to assign special importance to the color flavor of the cell.

![](../.gitbook/assets/statistics.PNG)

## Inhomogeneous simulation parameters



![](<../.gitbook/assets/inhomogeneous parameters.png>)
