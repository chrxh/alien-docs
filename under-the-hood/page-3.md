# Architecture

## Overview

At the coarsest level, the source code can be structured into targets (libraries and executables) and their dependencies. The graphical user interface and the engine are completely decoupled. For example, it would be possible to use a different backend instead of CUDA.

![Dependencies of libraries (orange) and executables (green)](../.gitbook/assets/packages.svg)

The `Base` library is used by all others and therefore is not separately marked with dependency arrows.&#x20;

## Engine

The main classes of the engine libraries and their relationships are shown in the following diagram. The CUDA code is completely encapsulated in the `EngineGpuKernels` library.

![Engine classes and their dependencies](../.gitbook/assets/engine.svg)

The simulation code for calculating the next time step is located in `SimulationKernelsLauncher`.

The data for a simulation are encapsulated in different sets of classes/structs on the CPU as well as GPU side. For the data transfer in both directions, the `DataConverter` translates the `Description` objects into separate transfer objects (TOs) consisting of C arrays, and vice versa.

![Main data structures for storing the simulation data](../.gitbook/assets/data.svg)

For some use cases it is more convenient to utilize a `ClusteredDataDescription` instead of a `DataDescription` on the CPU side. The difference is that the `ClusteredDataDescription` consists of `ClusterDescriptions`, which in turn contain `CellDescriptions` that are connected to each other.

## GUI

The user interface is developed with [Dear Imgui](https://github.com/ocornut/imgui). All windows and dialogs that can be displayed are encapsulated in independent classes. The controller classes manage processes in the background or further windows. MVC patterns are not used in order not to unnecessarily bloat the code.

![Gui classes and some of their dependencies](../.gitbook/assets/gui.svg)
