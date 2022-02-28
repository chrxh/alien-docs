# Simulation Model

The implemented particle engine combines two different concepts for the simulation of matter and its dynamics, which can be regarded as two distinct layers.

### Physics Layer

On the physical level, soft bodies and to some extent rigid bodies and fluids can be simulated using particles. In ALIEN these matter forming particles are denotes as cells and their dynamics are the result of simple physical laws. Cells have the ability to form connections with other cells. Without a bond, two cells repel each other when they approach. If a bond exists, the cells are held together with a force proportional to the deviation from a reference distance. The situation is more complicated when a cell has multiple bonds to neighboring cells. In this case, forces also arise when the angles between the different bonds deviate from a reference configuration. In this way, a structure can bend back to its original configuration after a certain period of time during which it has been subjected to (moderate) deformations.

Cell connections can be formed and destroyed. If a collision of two particles occurs and if the impact velocity exceeds an (adjustable) threshold, a connection can be established if both cells are permitting it. As soon as a cell connection is created, the reference distance and, if necessary, the reference angles are calculated and cannot be changed under normal circumstances. Conversely, if a connection between two cells already exists and the actual distance deviates too much from the reference distance, the connection will be dissolved.

Thermal radiation is simulated by special particles, which are denoted as energy particles in the following. Each cell has an internal energy value, which can also be thought of as a temperature value. The higher the energy of a cell, the more energy it radiates into its environment in the form of energy particles. In this spirit, heat conduction within a cell cluster is not explicitly modeled, but results from the exchange of energy particles. Cells can be transformed into energy particles and vice versa when the energy value falls below or exceeds a critical value, respectively.

Large rigid bodies can only be simulated very inadequately with the described model, since momentum changes require a longer time to cover the entire body.

### Information Processing and Action Layer

