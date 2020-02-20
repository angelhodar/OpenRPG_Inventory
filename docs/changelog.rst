Changelog
=========

Improvements
------------

* Reworked save and load functionality using GameInstance as the manager to keep data across levels
  and dump desired data to disk. Before, components were able to save data directly to disk, but its
  better to let the GameInstance handle that for flexibility.
* Added function ``EquipFromContainer`` to abstract container origin (not only player inventory), so now an item
  can be equipped directly from any container like storage for example.
* Added function ``UpdateEquipmentVisuals`` to encapsulate all the visuals functionality.
* Removed ``OnSaveExtraData`` and ``OnLoadExtraData`` events for child container types, now to expand
  save and load functionality (for example player's inventory money) just override the ``SaveContainer``
  and ``LoadContainer`` functions to add the necessary code.
* Added ``OnEquipmentSlotDrop`` event with default functionality already implemented (unequip basically), but can be overriden
  to suit specific needs.
* Added function ``CanBeUsed`` in ``BP_BaseItem`` to remove the ``UsedSuccessfully`` boolean. Now its easier to override if an
  item should be used or not.
* Event ``OnItemUsed`` in ``BP_BaseItem`` is now called ``OnStartItemEffect``.
* Added events ``OnFinishItemEffect`` and ``OnItemUseFailed`` in ``BP_BaseItem``.

Bugfixes
--------

* Fixed bug where non equippable items were used when dragged to an equipment slot.


TODO
----

- Add widget to show keyboard controls and shotcuts when using the system.
- Improve the example scene.
- Add some real functionality to an item instead of just explaining how to do it.
- Add functions to dynamically increase the amounts of slots in container.