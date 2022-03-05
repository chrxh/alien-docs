# Construct simple worlds

#### Abstract

The aim here is to learn how to create own worlds filled with different colored bodies consisting of simple geometric shapes or freehand drawings. We will also make use of predefined patterns. In the process, we will familiarize ourselves with a multiplication function that allows us to mass-multiply arbitrary patterns with adjustable randomness.

## Start with an empty world

The first step for our own world is to create a new empty world via the _Simulation_ menu and then _New_. In the dialog we can set the dimensions and adopt the simulation parameters and symbols from the previous simulation. A dimension of 1000 x 1000 units is sufficient for our purposes for now. Furthermore, we set the settings to default by not adopting them.

{% hint style="info" %}
Please note that the length units do not represent pixels in the strict sense. The world is treated as a continuum. A length unit is rendered as one pixel at a zoom level of 1.0.
{% endhint %}

{% hint style="info" %}
It is also possible to resize a world afterwards. For this purpose there is a resize function in the _Spatial control_ window. We will explain this in a later article in more detail.
{% endhint %}

Then we open the simulation parameters window and set the _Radiation strength_ to 0, so that our constructions will last for a long time.

## Create cell clusters

We open the _Creator_ via the _Editor_ menu. This window provides various tools with which new cell structures can be created. It is recommended to try all functions in sequence:

* Create single energy particle
* Create single cell
* Create rectangular cell cluster
* Create hexagonal cell cluster
* Create disc-shaped cell cluster
* Draw freehand cell cluster

Except for the freehand drawings, all builds work the same way: One sets the properties in advance (e.g. the dimensions for a rectangular cell cluster) and then clicks _Build_. The cell cluster or energy particle is then generated near the center and automatically selected. This allows one to change the color, velocity or other properties immediately afterward in the _Pattern editor_. Even if you want to delete the generated pattern, you can also accomplish this via the _Pattern editor_ or press DEL.

![Some geometric primitives](<../.gitbook/assets/geometric primitives.png>)

In order to draw freehand, the drawing mode must be activated and explicitly deactivated when one is finished. As soon as it is activated, one can place cells in the simulation view with the left mouse button pressed.

![Freehand drawing](<../.gitbook/assets/freehand drawing.png>)





## Multiply structures
