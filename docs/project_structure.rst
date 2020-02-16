Project Structure
=================

This section will cover the project folder structure and a brief description of the main files on it,
to help you get more comfortable when looking at the project.

When you download it from `GitHub <https://github.com/angelhodar/OpenRPG_Inventory>`__ (after leaving a star :P)
and you open it with Unreal Engine, the first thing you will see at the root of the project are the ``Demo``,
``OpenRPG_Inventory`` and ``OpenRPG_Equipment`` folders. Lets quickly see what each one contains:

Demo
----

This folder contains blueprints, icons, materials, widgets, stuff from the *Third Person Template* and other assets
used just to test and explore the system. Lets focus on the blueprints and widgets folders as the other ones are not
relevant to the system functionality itself:

Blueprints
^^^^^^^^^^

Here you will find the implementation of the main game blueprints (character, player controller, game instance, etc).
They will help you a lot when you have to implement the system into your own project, because all of them
has the needed implementation to make the system work (components initialization, save/load, connection with the UI, etc).
The ``BP_DemoCharacter`` also has a few debug controls to test the system by yourself.

There are also other blueprints used to test some of the already implemented containers, like the ``BP_DemoStorage``
to help you understand how to create your own storage actors or ``BP_DemoShop`` which implements a common shop keeper.

Lastly, you can also find a folder with all the classes for each of the example items created. Dont worry about them at
the moment because later you will learn how to add your custom functionality to the items. Same applies to the character,
player controller and so on. I will cover how to integrate the system with them in each system's section. 

Widgets
^^^^^^^^^^

Here you will find some clean demo widgets like the interaction tooltips, the windows that contains the items grid, etc.
But the most important one is the ``WB_DemoMain``, because its the widget added to the viewport and displayed in the game,
which contains all the other widgets. That is, instead of creating one window for player inventory, another one for storage
and then adding each of them individually to the viewport, you just manage them in this main widget, adjusting them easily
as you want. When this one is added to the viewport, the rest of the widgets are added too, and its very easy to access them
if you need just getting a reference to the main widget.

.. Note:: Its a good practice to create a main HUD widget as the ``WB_DemoMain`` as explained before. However, this system doesnt
   care about how you manage your widgets. You will learn how this can be done in further sections.

OpenRPG_Inventory
-----------------

This folder contains all the blueprints, data structures, datatables and widgets needed to make this system work. In other
words, its the core of the system. All the components, base item classes, interfaces, functions library and so on are located
under the ``Blueprints`` folder, which as you can suppose, is by far the **most important folder** in the whole project.

There are other folders like the ``Structs`` and ``Enums`` that contains all the data structures and extra data types used by
the system, as well as a small items database using this data structure in the ``DataTables`` folder.

Finally, the widgets folder contains the most important widgets of the system: the item slot and the slots container grid.
Both handle most of the UI functionality with the components. Here you will also find the tooltip widget, showed when the mouse
is over an item slot to show information about the item it contains.

OpenRPG_Equipment
-----------------

Finally, as the name suggests, this folder groups all the equipment functionality, with the same schema as the
``OpenRPG_Inventory`` folder. This system was created with the design of the inventory system always in mind,
so you will find a lot of similarities when diving into the folders, but with much less complexity.