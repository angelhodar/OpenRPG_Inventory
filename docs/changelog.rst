Changelog
=========

Improvements
------------

* Reworked save and load functionality using GameInstance as the manager to keep data across levels
  and dump desired data to disk.
* Added function EquipFromContainer to abstract container origin (not only player inventory).
* Added function UpdateEquipmentVisuals to encapsulate all the visuals functionality.
* Removed OnSaveExtraData and OnLoadExtraData events for child container types, now to expand
  save and load functionality (for example player's inventory money) just override the SaveContainer
  and LoadContainer functions to add the necessary code.
* Added OnEquipmentSlotDrop event with default functionality already implemented (unequip basically), but can be overriden
  to suit specific needs.

Bugfixes
--------

* Fixed bug where non equippable items were used when dragged to an equipment slot.