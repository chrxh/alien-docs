---
description: >-
  Warning: This documentation is out of date and does not describe the behavior
  of the latest major version 4, which implements a new model. An up-to-date
  documentation can be found in the program help.
---

# Simulation model

The implemented particle engine combines two different concepts for the simulation of matter and its dynamics, which can be regarded as two distinct layers.

### Physics layer

From the physical perspective, soft bodies and to some extent rigid bodies and fluids are simulated using particles. In ALIEN these matter forming particles are denoted as cells and their dynamics are the result of simple physical laws. Cells have the ability to form connections with other cells. Without a bond, two cells repel each other when they approach. If a bond exists, the cells are held together with a force proportional to the deviation from a reference distance. The situation is more complicated when a cell has multiple bonds to neighboring cells. In this case, forces also arise when the angles between the different bonds deviate from a reference configuration. In this way, a structure can bend back to its original configuration after a certain period of time during which it has been subjected to (moderate) deformations.

Cell connections can be formed and destroyed. If a collision of two particles occur and if the impact velocity exceeds an adjustable threshold, a connection can be established if both cells are permitting it. As soon as a cell connection is created, the reference distance and, if necessary, the reference angles are calculated and cannot be changed under normal circumstances. Conversely, if a connection between two cells already exists and the actual distance deviates too much from the reference distance, the connection will be dissolved.

Thermal radiation is simulated by special particles, which are denoted as energy particles in the following. Each cell has an internal energy value, which can also be thought of as a temperature value. The higher the energy of a cell, the more energy it radiates into its environment in the form of energy particles. In this spirit, heat conduction within a cell cluster is not explicitly modeled, but results from the exchange of energy particles. Cells can be transformed into energy particles and vice versa when the energy value falls below or exceeds a critical value, respectively.

{% hint style="info" %}
During all simulated physical processes and cell activities the **conservation of energy is fulfilled**.

Energy in this context includes the internal cell and token energy as well as the energy from energy particles but not kinetic energy.
{% endhint %}

Larger rigid bodies can only be simulated very inadequately with the described model, since momentum changes require a longer time to spread over the entire cell structure. For this reason, an additional processing step can be optionally unlocked, which periodically adjusts the velocities of parts of cell clusters to a rigid body motion. This additionally stabilizes the cell structures and transmits impulse changes more quickly.

### Information processing and action layer

Complex behavior patterns such as foraging, self-replication, controlled movements or information processing may require an immense effort to recreate by using simple particle motions and artificial chemistries. In order to make such interesting behaviors easily accessible, cells can be equipped with a wide range of higher-level functions. A [Petri-Net](https://en.wikipedia.org/wiki/Petri\_net)-related model is used for the  coordination of the execution of cell functions and the communication between adjacent cells.

For this purpose tokens come into action. They are each assigned to a specific cell and jump to a neighboring cell (if possible) after each time step. To define flow directions for the token movements in the graph of cell clusters, numbers (by default from 0 to 5) are assigned to each cell. A token can only jump from a cell with value `a` to a connected cell with value `b` if `(a + 1) mod 6 = b` is fulfilled. Another constraint is that each cell can only hold a maximum number of tokens.

![Example for token movements](../.gitbook/assets/tokenmodel.svg)

As soon as a token passes a cell, the function of the underlying cell is executed. Each cell function requires certain input information and provides an output, which in both cases are obtained from the token memory. For example, a sensor function needs to know the mass density and cell type (cell color) to be searched for, and will provide the angle and distance in case of success. All these information are stored in the token memory.
