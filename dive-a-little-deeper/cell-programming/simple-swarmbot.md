# Simple swarmbot

#### Abstract

Cells in ALIEN can perform a wide variety of actions. We will address mass sensors and motion control in this section. These functions will be explained by building a simple swarm robot that scans its environment for particle concentrations with a specific color and moves in that direction.

## Build simple skeleton

A simple skeleton for our purpose consists of a loop-shaped structure in which a token can circulate. In this structure, we need a _muscle_ on both sides that provides us with an impulse depending on the direction we want to direct. We also need to accommodate a sensor that will give us the distance and angle where particle concentrations of a certain color are located.

![Skeleton of a simple swarmbot](../../.gitbook/assets/skeleton.svg)

The above structure is composed of 7 cells and consists of 3 functional units:

