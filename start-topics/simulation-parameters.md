# Simulation parameters

#### Abstract

By adjusting simulation parameters we can customize the physical laws as well as cell functions and mutations. ALIEN offers the possibility to vary such parameters spatially as well as temporarily. This allows us to create diversified worlds, which are especially interesting for evolutionary simulations because different parameters require different evolutionary adaptations. Here we want to explore some possibilities for setting simulation parameters and their effects

## Overview

The simulation `./examples/simulations/Complex Fluids.sim` is suitable for testing different parameter settings. We open the simulation parameters window and should see somewhat as follows:

![Window for simulation parameters](../.gitbook/assets/window.png)

In this window there is a tab widget with a default tab named _Base_. This tab contains the parameters which apply everywhere where no special spots have been set up. We will go into more detail about this, but so far we have not set up any spots. Furthermore, at the bottom of the window the toggle named _Change automatically_ can be used to vary the parameters in time.

Basically, changes to the parameters become active immediately and can also be carried out during a running simulation. By clicking the button next to the slider, the corresponding parameter can be reset to their initial state at any time.

## Adjust important physical parameters

We would like to focus on a few physical parameters and describe their effect in the following. The other parameters responsible for mutations and cell functions we will explored later. We recommend to run the loaded simulation and to play around with the sliders to the associated parameters.

* _Friction_: This value indicates how much the particles are decelerated in each time step. If this value is high, all movements quickly come to a halt. As a result, strong adaptive pressure is generated in evolutionary simulations, favoring individuals that are able to move quickly.
* _Rigidity_: Since ALIEN is based on a pure particle engine, rigid bodies cannot really be simulated. Nevertheless, in order to approximate rigid motions, an additional processing step can be switched on with this parameter, which requires some extra computation time (typically about 30%).
* _Radiation strength_: A high radiation leads to rapid energy losses of the cells and ultimately to their decay. If the radiation is too strong, stable structures cannot exist for a longer time and the simulation quickly reaches maximum entropy.
* _Maximum force_:
* _Binding creation force_:
* _Binding maximum energy_:

