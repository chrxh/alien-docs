# Self-replicating machines

#### Abstract

There are several ways to create self-replicating structures. In this article, machines with the ability to self-replicate by inspection will be described. On the one hand they need a mechanism to read out their own structure and internal states and, on the other hand, they also require an apparatus to replicate them.

## Cell skeleton

We build our self-replicating machine as a simple loop. A more complicated topology is of course also conceivable, but not relevant for our rather minimal example. In general, replication costs energy and since energy conservation must be satisfied in ALIEN, in addition to the ability to self-replicate, we also need simple movement and digestion functionality so that sufficient energy can be provided.

![Skeleton of a simple self-replicating loop](<../../.gitbook/assets/skeleton replicator.svg>)

A possible basic framework is shown above. At the front (right) is a cell with attack capabilities and at the sides are muscle units to accelerate in the respective direction. For simplicity, we will implement a straight ahead movement pattern. At the back (left) we attach a scanner cell to read out the inner structure and a constructor cell to rebuild the extracted information. The challenge here is that we have a variety of cell types and we need to provide them with the appropriate information using the computational cells.

In the ALIEN editor, our self-replicator then looks like this:

![Realization of a self-replicating loop in ALIEN](<../../.gitbook/assets/loop closeup.png>)

In the following, we will first explain the two new cell types (Scanner and Constructor) and then discuss the data supply.

## Working principle of a scanner cell

A scanner cell can read the internal state and the angles and distances of the reference configuration to another cell in the cell cluster. For this purpose, the scanner cell numbers all the cells in the cluster starting from itself according to the specified order. If one wants to read out a cell in the cluster, one has to tell the scanner cell the corresponding number. Cells are numbered in a spiraling counterclockwise fashion around the scanner cell. A few examples illustrate the numbering algorithm:

![Numbering example 1: rectangular cell cluster](<../../.gitbook/assets/numbering 1.svg>)

In this example, the scanner cell is on the blue token that comes from the left neighboring cell. The scanner cell itself is numbered with 0 and the cell where the token comes from with 1. Afterwards the further cells are numbered counterclockwise in ascending order.

{% hint style="warning" %}
The numbering shown here has nothing to do with the token branch numbers of the cells.
{% endhint %}

![Numbering example 2: rectangular cell cluster with different position of scanner cell](<../../.gitbook/assets/numbering 2.svg>)

However, in this example, the cell cluster is not completely covered by the numbering algorithm,

![Numbering example 3: loop-shaped cell cluster](<../../.gitbook/assets/numbering 3.svg>)

For our replicator, the resulting numbering of the cells is relatively simple. With the help of this (relative) numbering, the scanner cell can now be provided with a number indicating for which cell in the cluster the information should be read out.

## Working principle of a construction cell

