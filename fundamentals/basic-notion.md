# Basic Notion

Generally, all bodies as well as radiations are modeled via different types of particles within an ALIEN simulation. The following terms are frequently used in this documentation.

### World

An ALIEN world is two-dimensional rectangular domain with periodic boundary conditions. The space is modeled as a continuum.

### Cell

Cells are a type of particles which serve as matter building blocks and which are able to connect to each others. One can think of cells as nodes and the connections as edges of a graph embedded in a 2D space. Moreover, cells possess physical properties such as

* Position in space
* Velocity
* Internal energy (corresponding to its temperature)
* Upper limit of connections

and a specialization together with an internal state.

### Cell specialization

Each cell has a special function that can be triggered and (usually) accepts certain inputs and returns output values. Currently, the following functions are implemented:

* Computation: Allows the execution of 15 lines of assembler-like code.
* Construction: Can create a new cell with or without a connection to the host cell.
* Digestion: Converts a surrounding cell to internal energy under certain conditions.
* Sensor: Scans the vicinity or a particular direction for concentration of particles with a certain color.
* Muscle: Can contract or expand a cell connection. During this process, it can generate a momentum.
* Scanner

