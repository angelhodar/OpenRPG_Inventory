Save / Load
===========

In this section we will be covering one aspect that is common for the inventory and equipment
system: **the built-in save and load functionality**. It is important to understand how both systems
(specially containers) handles their data to be persistent **even when the game is closed** and how
that data is **organized** in the blueprints that take care of this work.

When we talk about save and load functionality, **2 aspects** must come to your mind:

* Data persistent **across different maps** and linked to the **current game session**.
* Data persistent **across different game sessions**.

To explain this concepts better, lets see which blueprints are related to each one.

GameInstance
------------

This blueprint has the property of being persistent across maps. That means that if your player travels to a new map
and the items container actors in the old map gets destroyed (and also the player), then all the data they
holded in the old map would be lost, but **this blueprint is the same instance always across different maps**. 
Because of that, its the perfect place to keep all the data persistent even if the player goes to a different map. 

In this project, the ``BP_DemoGI`` is used with the purpose explained before. Further we will see the
functions, interfaces and variables it uses to act as we want.

However, all the save and load functionality isnt complete, because if the game is closed then the game instance
is also destroyed, so the saved data there would be lost when we open the game later. We would need something
like an external file on the hard drive to store the data we want to keep across different game sessions. For that reason, we need another
kind of blueprint, which is the ``SaveGame`` class.

SaveGame
--------

This blueprint is a special engine class created for the purpose we need. If we want to save or load something from an
external file, Unreal can create a file with the ``.sav`` extension, which can hold all the data we need to keep across
game sessions. The interface with that file is just an instance of the class ``SaveGame``, so we just need to create a
custom instance and add there all the variables we need to keep, just like a normal actor.

The instances created for this project are:

* ``InventorySave``: It holds all the variables needed to keep all the items containers and the player data related to
  the inventory functionality.

* ``EquipmentSave``: Holds all the variables needed for the equipment system.

.. Attention:: Please give a look at the functions used to interact with this type of class `here <https://docs.unrealengine.com/en-US/Gameplay/SaveGame/index.html>`_

.. Note:: You may be wondering why the ``GameInstance`` blueprint used in this project is part of the demo content and doesnt
   come in the ``OpenRPG_Inventory`` folder if it is such an important blueprint for the save and load system to work
   properly. That is because you will probably have your own ``GameInstance`` already implemented with your own logic,
   so I prefer to give you the tools to easily integrate the logic into your own class rather than obey you to use the
   ``BP_DemoGI``. Of course, if you are not using a custom ``GameInstance`` in your project at the moment, you can perfectly use
   this one.
  
Now that you understand the main blueprints used by this system and why they are used, lets see how they are connected
between them and how the containers and the player sends and receive data from them.

Interfaces
----------

To make the communication as transparent as possible, I have provided a few blueprint interfaces to abstract the
communication between the components and your game instance. These interfaces are:

* ``BPI_ContainerSave``
* ``BPI_PlayerInventorySave``
* ``BPI_EquipmentSave``

Each of them have 2 functions with the syntax **SaveXXXX** and **LoadXXXX** depending on the type of data they save.
For example, ``BPI_EquipmentSave`` has the functions ``SaveEquipment`` and ``LoadEquipment``, while the interface
``BPI_ContainerSave`` has the functions ``SaveContainer`` and ``LoadContainer``.

Those functions have a common input parameter called ``SaveName``, which is a string label that **identifies** the data that you are going to save or the data
you want to load. Think of the data as a **package** and this string as the **ID** of that package. This concept is very important because when you want to save or
load any actor data, you need to pass this string to let the ``GameInstance`` identify what data package should be loaded or how it should be saved. You can just
create an editable string variable in the actors that have any component data you want to handle (storage actors, the player, etc), and then use it when you
save or load any data.

.. Note:: In the ``BPI_ContainerSave`` interface you will notice there is an extra boolean input called ``DiskSaveable`` in the ``SaveContainer`` function.
   That is used to avoid saving containers that you would not want to be saved on disk. For example, you probably dont want to save the loot from a monster
   in the disk, but a storage or the player inventory should be.

There is also an extra interface called ``BPI_SaveManager``. This one is used by the ``GameInstance`` to communicate with the ``SaveGame`` classes. Following
the same schema as the other interfaces, it has the functions ``SaveDataToDisk`` and ``LoadDataToDisk``. However, this functions doesnt have any input or output
parameters, they are used to save or load a state of your game to the disk. Because of this, ``LoadDataToDisk`` can be called only when the game starts to dump all
the saved data to your game instance, and then work with the data there. By the other hand, the ``SaveDataToDisk`` can be called when you reach some checkpoint in
your map, or just when a UI menu button used to save the game is clicked.

If you are still reading this, congratulations! At the moment, you know which classes are used in the saving and loading process and why. Now you just need to add
the interfaces commented above to your game instance and implement them with the data structure variables you prefer. My recommentation would be to use a **map**
variable type, which is also called as **dictionary**. That is because the data stored has the structure of SaveName -> Data, which is the structure that this data
type is made for, and the blueprint code needed is just a few nodes and works very fast. Just give a look at the ``BP_DemoGI`` blueprint and you will see how I have used
it!







