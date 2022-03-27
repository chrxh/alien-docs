# Digestion

#### Abstract

In ALIEN, a digestion process refers to the conversion of a foreign cell into usable energy and can also be considered as a form of attack. This capability for energy consumption are required by cell clusters to have a functioning metabolism. To explain its functioning and implementation, the swarmbot from the previous article will be upgraded and equipped with an attack function.

## Cell skeleton

We do not need to change the basic structure, but we will adjust the cell functions and the control logic a bit. First of all, we need to accommodate a digestion unit. The front side of the machine is ideal for this because it will be in contact with other cells most frequently. In our case, it will look like this.

![Cell skeleton of a swarmbot with attack capabilities](<../../.gitbook/assets/skeleton attacker.svg>)

As one can see, we have to sacrifice a computational cell for this purpose. However, we still have a cell available at the bottom center, which we had not used so far. Before we get to the implementation details, let us give a more detailed explanation of the digestion process.

## Working principle of a digestion cell

