# Digestion

#### Abstract

In ALIEN, a digestion process refers to the conversion of a foreign cell into usable energy and can also be considered as a form of attack. This capability for energy consumption are required by cell clusters to have a functioning metabolism. To explain its functioning and implementation, the swarmbot from the previous article will be upgraded and equipped with an attack function.

## Cell skeleton

Let us adopt the swarmbot from the last article and modify it to our purposes. The basic structure does not need to be changed, but we will adjust the cell functions and the control logic a bit. First of all, we need to accommodate a digestion unit. The front side of the machine is ideal for this because it will be in contact with other cells most frequently. In our case, it will look like this.

![Cell skeleton of a swarmbot with attack capabilities](<../../.gitbook/assets/skeleton attacker.svg>)

As one can see, we have to sacrifice a computational cell for this purpose. However, we still have a cell available at the bottom center, which we had not used so far. Before we get to the implementation details, let us give a more detailed explanation of the digestion process.

## Working principle of a digestion cell

The basic principle is simple: As soon as a digestive cell is triggered by a token, it searches for cells in the immediate vicinity that are not connected to it directly or via another cell. For each of these matched cells, it is calculated how much internal energy can be drawn from it. However, the amount of energy drawn depends strongly on the simulation parameters and the digestion configuration in the token memory. In the worst case, the digestion cell even loses energy if the foreign cells do not meet certain criteria. Let us discuss the corresponding simulation parameters under _Cell specialization: Digestion function_:

#### Energy cost

If we have set energy cost greater than 0, then after each digestion process, even if no neighboring cells were found, the cell loses the energy specified in this parameter and in return releases an energy particle with this energy. Thus, a large value penalizes structures that attack other cells on a massive and unselective basis.

#### Target color mismatch penalty

This parameter (among others) assigns a special meaning to the color of a cell. One can also think of the cell color as another form of typification, which can contribute to more diverse ecosystems. In the token memory, a specific color can be set for the cells that are aimed to be digested. This effect will be activated with the _Target color mismatch penalty_ parameter if it is greater than 0. If the color of the cell to be digested does not match the specified color, less energy is drawn from it, depending on the value of this parameter. In the extreme case, when the parameter is greater than 1, the cell even loses energy when it tries to digest cells with the wrong color.

#### Successive color dominance

This parameter controls a process which compares the color of the digestion cell with the color of the cell being digested. Each color can be assigned a numerical value between 0 and 6. We say that a color `a` is the successor of another color `b` if `a ≡ b + 1 (mod 7)` holds true.

![](<../../.gitbook/assets/color dominance.svg>)
