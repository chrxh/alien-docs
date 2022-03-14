# Evolution experiments

#### Abstract

We will perform evolutionary simulations by injecting self-replicating machines into pristine worlds. Mutations will lead to gradual optimizations of the individuals. In this context, we want discuss the influence of crucial simulation parameters on cell functions. ALIEN offers advanced features like inhomogeneous parameter values, which we will also make use of. We will then address how larger self-replicating machines can be made functioning.

## Simple simulation setup for small self-replicators

The basic idea is simple: We create an empty world, fill it with enough particles serving as food source, inject a self-replicating machine and activate occasional mutations. The rest is done by the ongoing simulation.

We can already load a simple setup using the simulation file `./examples/simulations/evolution/Loops.sim`. Alternatively we create a new simulation with sthe ize 1000 x 500, fill it with enough particles (80,000 should be sufficient) and load the pattern `./examples/patterns/replicators/Loop.sim` into it. The self-replicating structure has a loop shape, can move randomly, eat other particles to obtain energy from its environment and copy itself by inspecting its own structure to rebuild it. Can you find the little particle machine right away?

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

![](<../.gitbook/assets/loop later.png>)

If you let the simulation run even longer, mutations are increasingly created that multiply faster or move differently. The color also changes more or less randomly. An example of a longer simulation run can be found in the file `./examples/simulations/evolution/Loops Evolved.sim`.

{% hint style="info" %}
To increase the simulation speed, one can disable _Render simulation_ in the _View_ menu..
{% endhint %}

## Increase diversity through color semantics for cell types

It can be observed that after some time a certain equilibrium develops. The population size remains roughly stable, gradually fewer traits are changing and evolutionary leaps become rarer. One way of regularly breaking through equilibria and creating more refuge areas is to assign special importance to the color flavor of the cell.

![](../.gitbook/assets/statistics.PNG)

## Inhomogeneous simulation parameters



![](<../.gitbook/assets/inhomogeneous parameters.png>)

## Simulations with larger self-replicators
