Inventory System
================

In this section we will explore the inventory system and how to use it. Let me first explain you that when this
project started, this system was just purely that, an inventory system that was attached to the main player character.

However, as long as my programming knowledge was improving, I decided to generalize this system to make it what it is
now, an **items container** system that can be attached to any actor, not just the player character. To achieve this,
I have made an extensive use of **component inheritance**, which is the key to get **flexibility** and **generic behaivour**
at the same time.

Blueprints
----------

Adding new container types
**************************

To create a new type of container different from the example ones, you have to follow this simple steps:

1. Create a new entry in the ``e_ContainerType`` enum under ``OpenRPG_Inventory/Enums`` folder.
2. Create a new items container grid widget to show the items coming from your new type of container.
   To do that, just open the ``WB_Main`` widget under the ``Demo/Widgets`` folder. Grab a ``WB_DemoWindow``
   widget and move it to the desired place. Now under the **Settings** category of that widget, modify the
   value of the ``ContainerType`` variable with the type of your new container.
3. Go to your player controller and in the functions ``GetContainerWidget`` and ``GetMainContainerWidget`` from the
   ``BPI_ContainerWidgets`` interface add your new widget window and its container to the return value.

Thats it! Now you have a new widget that will be updated with the containers of your new type. The new containers will
use the player controller to extract the necessary references from the widget you have added. Lets check now how to use
this new type creating a new container!

Creating a new container
************************

To create a new component, just navigate to the ``/OpenRPG_Inventory/Blueprints/Components`` folder and you will see there
is a ``BP_ItemsContainer`` which is the **base** for all the containers you create, apart from the example ones. To create
a new one, just right click that component and select **Create child**. Open that new component and now you will see you
have access to a few variables under the **Settings** category in the **Details panel**:

TODO: Extend and correct variables names

* ``ContainerType``: This sets the type that your new component is going to have.
* ``ContainerSize``: The amount of default slots that the container will have when initialized.
* ``SlotsPerRow``: The amount of slots that should be displayed per grid row in the UI.
* ``DefaultItemsRow``: Identifies a set of items that should be added automatically to the container when its initialized. Rows of this
  type can be created in the ``OpenRPG_Inventory/Datatables/DT_ItemsList``.
* ``AdaptSize``: If true, the ``ContainerSize`` value will be ignored and the size will be adjusted to the size of the items set you defined
  for your ``DefaultItemsRow``. If the row is not valid then this setting has no effect.
* ``StackSplitAmount``

Just customize them as you need. Then its time to customize some of your new container's behaivour by overriding a set of functions
that will be called under certains events:

TODO: Add the rest and explain overridable functions

* ``OnSlotClicked``: Called when a slot is right clicked in the UI. You can see some implementation examples in the
  example components. In the case of the ``BPC_PlayerInventory``, it executes the functionality of using an item, and
  in the case of the storage, it moves the item in that clicked slot to the player's inventory.
* ``HandleSlotDrop``: Called when an item slot is dropped from another container is dropped into an slot of this new container.
* ``HandleEquipmentSlotDrop``: Same idea as before but only executed when this drop comes from an equipment slot.
* ``SaveContainer``: Add extra behaivour when saving data from this container. For example, in ``BPC_PlayerInventory``, the
  player's money is also saved when calling this function.
* ``LoadContainer``: Same idea as above but for loading purposes.


Adding items container to an actor
**********************************

TODO: Explain the process and the initialization pipeline.


Example containers
******************

TODO: Explain each of the default containers.



Interfaces
----------


Data Structure
--------------


Widgets
-------




