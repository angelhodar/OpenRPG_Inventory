# OpenRPG: Inventory System
#### Hi! In this repository you will find an easy way to manage a simple and expandable inventory. Everything is commented and structured to be easy to learn.

  - Comes with 28 functions (23 public and 5 private) that allows you to simply manage the inventory. 
  - Supports different types of items (consumable, equipment, material, quest, miscellaneous and loot). You can add your custom ones!
  - Items are stored in a DataTable, each row is identified by a number (the ItemID), and contais the data of the item. Its very easy to add and modify your own items! 
  - Each usable item can execute custom logic, just overriding an event in its class.
  - 15 example items.
  - Drag & Drop functionality.
  - Clean UI example.
  
 ### How to create new items:
 1. Create a new row in DT_Items with a new ID that you want to identify that item. 
 2. Fill the info with your custom one.
 3. If that item is going to execute some logic when used, go to the MasterClasses folder an create a child blueprint class from the master class of your new item type. Give it a name and inside of it just override the event "OnItemUsed" with your preferences.
 4. Set that class in the data of the item.
 5. Also if your item is a loot or equipment item, go to DT_Loot, create a new row with the name you want in their appropiate table filling the info. Then add that name to the appropiate variable at the end of the item data.
 6. Enjoy!
 
  Icons from:
  - http://www.ludicarts.com/free-rpg-icons/
  - http://www.ludicarts.com/free-rpg-icons-2/
