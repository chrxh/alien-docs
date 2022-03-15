# Simulation parameters

#### Abstract

By adjusting simulation parameters we can customize the physical laws as well as cell functions and mutations. ALIEN offers the possibility to vary such parameters spatially as well as temporally. This allows us to create diversified worlds, which are especially interesting for evolutionary simulations because different parameters require different evolutionary adaptations. Here we want to explore some possibilities for setting simulation parameters and their effects.

## Overview

The simulation `./examples/simulations/Complex Fluids.sim` is suitable for testing different parameter settings. We open the simulation parameters window and should see somewhat as follows:

![Window for simulation parameters](../.gitbook/assets/window.png)

In this window there is a tab widget with a default tab named _Base_. This tab contains the parameters which apply everywhere where no special spots have been set up. We will go into more detail about this, but so far we have not set up any spots. Furthermore, at the bottom of the window the toggle named _Change automatically_ can be used to vary the parameters in time.

Basically, changes to the parameters become active immediately and can also be carried out during a running simulation. By clicking the button next to the slider, the corresponding parameter can be reset to their initial state at any time.

## Adjust physical parameters

We would like to focus on a few physical parameters and describe their effect in the following. The other parameters responsible for mutations and cell functions we will explored later. We recommend running the loaded simulation, playing with the sliders of the associated parameters and applying forces with the mouse pointer to observe the effects.

* _Friction_: This value indicates how much the particles are decelerated in each time step. If this value is high, all movements quickly come to a halt. As a result, strong adaptive pressure is generated in evolutionary simulations, favoring individuals that are able to move quickly.
* _Rigidity_: Since ALIEN is based on a pure particle engine, rigid bodies cannot really be simulated. Nevertheless, in order to approximate rigid motions, an additional processing step can be switched on with this parameter, which requires some extra computation time (typically about 30%).
* _Radiation strength_: A high radiation leads to rapid energy losses of the cells and ultimately to their decay. If the radiation is too strong, stable structures cannot exist for a longer time and the simulation quickly reaches maximum entropy.
* _Maximum force_: If the force acting on a cell is greater than this value, the cell and their connections to neighboring cells will be destroyed. A high value consequently produces great amount of damage in an event of collisions.
* _Binding creation velocity_: When two cells collide, a new connection can be established if both cells still have a free space for a connection and the impact velocity exceeds a specific value that can be set with this parameter. It is easy to perceive that with a high value, the fluid in the simulation clumps very easily.
* _Binding maximum energy_: This value indicates up to what energy a cell can maintain connections. At very low values (below 100), most cell clusters break down into individual cells and all matter in the simulation behaves fluid-like.

We can observe the influence of changes of some parameters in the statistics function. For instance, if we drop the radiation to 0 there will be muss less energy particles as shown in the following.

![](../.gitbook/assets/statistics.png)

## Simulations with spatially varying parameters

There is a possibility to define special zones including transition areas where other simulation parameters can be set. Such so-called spots can be created by clicking on the + button next to the _Base_ tab. By default, the spots are circular, but they can also be made rectangular. To proceed we set the core radius to about 130 and the fadeout radius to 40 and should get the following:

![Simulation parameter spot](../.gitbook/assets/spot.png)

The parameters from the _Base_ tab are initially taken over in the spot, which we can now change. In the transition zones, whose distance is set with the fadeout radius, the simulation parameters are interpolated between the _Base_ and _Spot_ tabs.

{% hint style="warning" %}
Note that there are some parameters in the _Base_ tab which cannot be changed in a spot (e.g. maximum cell bonds).
{% endhint %}

## Varying parameters over time

A special feature that is particularly interesting for evolution experiments is the possibility to change simulation parameters over time. It is a well-known phenomenon that a population of individuals adapts to environmental conditions through evolutionary pressure, eventually reaching a kind of local optimum of fitness. To break these states of equilibrium, it is useful to change external conditions at regular periods. In ALIEN there is such an automatism, which can be activated with the _Change automatically_ toggle in the parameter window. If activated it does the following:

At first random target values for certain simulation parameters are chosen. Then the current parameter values are changed in slow steps towards this target. The duration of such a step can be configured in the window. If the parameter target is reached a new random target will be select.

Now it might happen that the population does not manage to adapt to the new conditions. To prevent this situation from becoming critical, all cell activities are measured regularly in the background and if these decrease significantly, e.g. because more and more individuals become extinct, the simulation parameters are turned back again and the target is approached again. If this procedure fails after the third attempt, an other target will be chosen.

We will discuss evolution simulations in more detail in a later article.
