# Spatio-Temporal Navigation

### Abstract

This first tutorial is intended to help one become familiar with the simulator if one has not used it before. One objective is to show the basic spatial and temporal navigation functions. For this purpose, we will load an existing simulation file from the examples provided. For the sake of simplicity, we will choose an example here where the cell clusters do not perform any additional actions. In general, it is possible to equip them with functions that allow programmable interaction with the environment.

### 1. Open an existing simulation

We open a prepared simulation file by clicking on _Simulation_ in the menu and then on _Open_. When the corresponding dialog appears we navigate to the directory `./examples/simulations/physics` and select `ALIEN.sim`. Generally, every ALIEN simulation consists of 3 separate files. In this case we have the following:

* `ALIEN.sim` -  This is the main simulation file and the one which is shown in the dialog. It contains every particle that is in the simulated world. It should be noted here that sim-files can also be loaded in the pattern editor. But in that case no settings and symbols are changed.
* `ALIEN.settings.json` - All simulation settings including world size, time step, simulation parameters and zones are stored here. These include, among others, physical parameters responsible for damaging, bonding or radiation of bodies. All this properties are encoded here in the JSON ([JavaScript Object Notation](https://en.wikipedia.org/wiki/JSON)) format and can thus be edited outside with any editor.
* `ALIEN.symbols.json` - In this file one finds a list of symbols and their defining values. Symbols are user-defined simple substitution rules and are used to simplify the writing ofsmall programs in a certain assembler-like language for computing cell functions. Symbols can be constants or variables.

\
