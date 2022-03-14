# Evolution experiments

#### Abstract

We will perform evolutionary simulations by injecting self-replicating machines into pristine worlds. Mutations will lead to gradual optimizations of the individuals. In this context, we want discuss the influence of crucial simulation parameters on cell functions. ALIEN offers advanced features like inhomogeneous parameter values, which we will also make use of. We will then address how we  larger self-replicating machines can be utilized.

## Simulation setup for small self-replicators

The basic idea is simple: We create an empty world, fill it with enough particles serving as food source, inject a self-replicating machine and activate occasional mutations. The rest is done by the ongoing simulation.

We can already load a simple setup using the simulation file `./examples/simulations/evolution/Loops.sim`. Alternatively we create a new simulation with sthe ize 1000 x 500, fill it with enough particles (80,000 should be sufficient) and load the pattern `./examples/patterns/replicators/Loop.sim` into it. The self-replicating structure has a loop shape, can move randomly, eat other particles to obtain energy from its environment and copy itself by inspecting its own structure to rebuild it. Can you find the little particle machine right away?

![Initial setup](../.gitbook/assets/loop.png)

Let us take a closer look at the loop and inspect its computation cells:

![Close up of the loop](<../.gitbook/assets/loop closeup.png>)

The cell cluster consists of 2 muscle cells for movement, a scanner cell for reading out the internal structure, a digestion cell for transforming surrounding particles into internal energy, a construction cell for creating new particles and several computational cells that are used for coordination. The exact replication process will be discussed in a later article. The cell code is also shown in the inspected cells.

## Inhomogeneous simulation parameters



![](<../.gitbook/assets/inhomogeneous parameters.png>)

## Simulations with larger self-replicators
