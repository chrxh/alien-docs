# Self-replicating machines

#### Abstract

There are several ways to create self-replicating structures. In this article, machines with the ability to self-replicate by inspection will be described. On the one hand they need a mechanism to read out their own structure and internal states and, on the other hand, they also require an apparatus to replicate them.

## Cell skeleton

We build our self-replicating machine as a simple loop. A more complicated topology is of course also conceivable, but not relevant for our rather minimal example. In general, replication costs energy and since energy conservation must be satisfied in ALIEN, in addition to the ability to self-replicate, we also need simple movement and digestion functionality so that sufficient energy can be provided.

![Skeleton of a simple self-replicating loop](<../../.gitbook/assets/skeleton replicator.svg>)

A possible basic framework is shown above. At the front (right) is a cell with attack capabilities and at the sides are muscle units to accelerate in the respective direction. For simplicity, we will implement a straight ahead movement pattern. At the back (left) we attach a scanner cell to read out the inner structure and a constructor cell to rebuild the extracted information. The challenge here is that we have a variety of cell types and we need to provide them with the appropriate information using the computational cells.

In the ALIEN editor, our self-replicator then looks like this:

![Self-replicating loop in ALIEN](<../../.gitbook/assets/loop closeup.png>)

In the following, we will first explain the two new cell types (Scanner and Constructor) and then discuss the data supply.

## Working principle of a scanner cell



## Working principle of a construction cell

