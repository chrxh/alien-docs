---
cover: .gitbook/assets/version3.png
coverY: 0
---

# What is ALIEN?

**A**rtificial **LI**fe **EN**vironment (**ALIEN**) is an artificial life simulation tool based on a specialized 2D particle engine in CUDA for soft bodies and fluid-like media. Each simulated body consists of a network of smart particles that can be enriched with higher-level functions, ranging from pure information processing capabilities to physical equipment (such as sensors, actuators, weapons, constructors, etc.) whose executions are orchestrated by a signaling system. The bodies can be thought of as agents or digital organisms operating in a common environment.

The program comes with

* Two-layered particle engine: The bottom layer simulates the thermo-mechanical behavior of soft bodies and their surrounding fluids, while a powerful information processing and action processor operates on the top layer.
* Vector graphics engine: The rendering is completely decoupled from the simulation engine. Sections of the simulated world are rendered as vector graphics and post-processed using shaders. The level of detail is adjusted with the zoom level. At a lower zoom level only the nodes are displayed, whereas at a higher levels, edges, information flows and (optionally) internal states are also visible.
* Particle editor: The properties and function of each particle can be modified. For example, editing windows can be pinned to several particles and even viewed while the simulation is running. A programming environment is provided for particles that are intended to perform computational operations.
* Graph editor: The components of existing bodies can be easily disassembled, rearranged and connected just by using the mouse. The graphs of new bodies can be created as geometric shapes or freehand drawings. Mass and scale operations facilitate the creation of large worlds.
* Extensive capabilities to control simulation parameters: It is possible to define different simulation parameters in spatial zones as well as to fluctuate them in time.

Main design goals:

* High performance for simulation and rendering through extensive use of CUDA and OpenGL.
* Good usability and an enjoyable user interface in spite of the high complexity of the simulation model and the wide range of setting options.
* Visually appealing post-processing of rendered simulation data.

