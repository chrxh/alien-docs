# Simple swarmbot

#### Abstract

Cells in ALIEN can perform a wide variety of actions. We will address mass sensors and motion control in this section. These functions will be explained by building a simple swarm robot that scans its environment for particle concentrations with a specific color and moves in that direction.

## Build a skeleton

A simple skeleton for our purpose consists of a loop-shaped structure in which a token can circulate. In this structure, we need a _muscle_ on both sides that provides us with an impulse depending on the direction we want to direct. We also need to accommodate a sensor that will give us the distance and angle where particle concentrations of a certain color are located.

![Skeleton of a simple swarmbot](../../.gitbook/assets/skeleton.svg)

The above structure is composed of 7 cells and consists of 3 functional units:

* The 2 cells on the left side are used to generate an impulse to steer to the right. One of these cells is a computational cell and is used to control the muscle cells. A muscle cell can only generate an impulse in the direction or opposite direction from which the token originates.
* We still need a similar unit on the right side. A forward impulse on the right side leads to a left steering of the total structure.
* In front of the swarmbot is our visual unit. It consists of a computational cell and a mass sensor.

We now construct the basic structure in the editor by creating 7 cells and connecting them individually. Because there are only 6 different token branch numbers, it is not possible to reproduce a directed cycle. Here we will help later with a special cell program. Furthermore, we create a token at an arbitrary cell. To this end, we inspect one of these cells in the pattern editor (shortcut ALT+N) and click on the tab with the plus symbol.

![Skeleton of our swarmbot in ALIEN](../../.gitbook/assets/skeleton.PNG)

We have now completed our basic scaffolding and can devote ourselves to the cell functions.

## Functioning of a muscle cell

Muscle cells can perform 4 different operations. The reference distance of the muscle cell to the predecessor cell is changed and, if necessary, an impulse is generated at the same time. The predecessor cell designates the cell from which the token originates that has just entered the muscle cell.

![The four different operations of a muscle cell](../../.gitbook/assets/muscle.svg)

The graphic above illustrates the different operations. Here we have two connected cells (a computation cell on the left and a muscle cell on the right) and a token that jumps from the left to the right cell and thus triggers the muscle function.

* The first operation refers to a pure contraction. Here, the reference distance of the cell connections is reduced by a fixed factor. This results in a force that brings the cells closer together.
* In the second case, the reference distance is also reduced and at the same time the muscle cell is given a forward impulse.
* The third operation describes a pure expansion. The distance between the connected cells is increased.
* Analogous to the second case, the fourth operation leads to an increase in distance and, at the same time, to a backward impulse of the muscle cell.

The indication of which operation should be performed is specified in the token memory. To simplify programming, there are default symbols for the memory location and its values.

