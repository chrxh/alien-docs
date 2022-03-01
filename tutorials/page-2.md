# Spatio-Temporal Navigation

### Abstract

This first tutorial is intended to help one become familiar with the simulator if one has not used it before. One objective is to show the basic spatial and temporal navigation functions. For this purpose, we will load an existing simulation file from the examples provided. For the sake of simplicity, we will choose an example here where the cell clusters do not perform any additional actions. In general, it is possible to equip them with functions that allow programmable interaction with the environment.

### 1. Open a simulation file

We open a prepared simulation file by clicking on _Simulation_ in the menu and then on _Open_. When the corresponding dialog appears we navigate to the directory `./examples/simulations/physics` and select `ALIEN.sim`. Generally, every ALIEN simulation consists of 3 separate files. In this case we have the following:

* `ALIEN.sim` -  This is the main simulation file and the one which is shown in the dialog. It contains every particle that is in the simulated world. It should be noted here that sim-files can also be loaded in the pattern editor. But in that case no settings and symbols are changed.
* `ALIEN.settings.json` - All simulation settings including world size, time step, simulation parameters and zones are stored here. These include, among others, physical parameters responsible for damaging, bonding or radiation of bodies. All this properties are encoded here in the JSON ([JavaScript Object Notation](https://en.wikipedia.org/wiki/JSON)) format and can thus be edited outside with any editor.
* `ALIEN.symbols.json` - In this file one finds a list of symbols and their defining values. Symbols are user-defined simple substitution rules and are used to simplify the writing of small programs in a certain assembler-like language for computing cell functions. Symbols can be constants or variables.

### 2. Spatial navigation window

After opening the file, the view is centered, the zoom level is set to 2.0 and the simulation is paused. By default the two windows _Spatial control_ and _Temporal control_ are visible on the right. If not they can be activated in the _Window_ menu. In this section, we are particularly interested in the spatial navigation window. You should see the following:

![Initial configuration after loading ALIEN.sim](<../.gitbook/assets/file opened.png>)

The purple color gradations in the background result from zones with different simulation parameters, but here they serve more as a visual decoration.&#x20;

By default, the navigation mode is enabled (or in other words: the editor is deactivated). In this situation we can navigate with the mouse as follows:

* If we press and hold the left mouse button, we zoom in the direction of the mouse cursor.
* If we press and hold the right mouse button, we zoom out.
* If we press and hold the middle mouse button, we can scroll by moving the mouse.

The zoom speed can be adjusted with the slider next to the label _Zoom sensitivity_ in the spatial control window. For large worlds, navigation via the scroll bar on the right and at the bottom of the simulation view are also useful, as well as the zoom icons in the window. When zooming in, one notices that more and more additional details are faded in:

* At the coarsest level, the cells and particles are displayed only as small dots.
* From a zoom level of 4 and more, connections between the cells can also be recognized.
* If you zoom in even further, the token pathways can be identified by arrows. Optionally further information can be displayed by activating the _Information overlay_ in the view menu. In this case also the cell specializations and token branch numbers are displayed as labels next to the cells.

![High zoom level with information overlay](<../.gitbook/assets/token pathways.png>)

For the sake of completeness, it should be noted here that the world size can be adjusted in the _Spatial control_ window. In addition, the view can be automatically centered on the selection (if there is one) when the simulation is running. For this purpose there is the toggle next to _Autotracking on selection_. We will discuss these functions in later tutorials.

### Temporal navigation window

