# 🧟 VEIN Beginner's Guide | Primer & Systems

![Vein, the game](assets/header.jpg)

[**Home**](index.md) | [**Survival Guide**](vein-client.md) | [**Server Guide**](vein-servers.md) | [**Media List**](public-domain-movies.md)

---

## Table of Contents
1. [Game Basics and Beginnings](#game-basics)
2. [Inventory and Equipment](#inventory)
3. [Inventory Classes](#classes)
4. [Base Building and Crafting](#building)
5. [Looting & Vehicles](#vehicles)
6. [Survival Tips](#survival-tips)

---

VEIN is a post-apocalyptic survival sandbox set in the northern reaches of New York State (Saranac, Redford, Dannemora, and Lyon Mountain). Your objective is long-term survival by managing **Resource Needs** (Food, Water, Shelter) and **Survival Needs** (Zombie Combat and Environmental Hazards). 

The game supports 1st and 3rd person views and allows for both single-player and multi-player experiences. You can start a world in single-player and later relaunch that same environment to play with friends. It can be run in PvP or PvE modes, offering players various ways to customize their gameplay style.

<a name="game-basics"></a>
## 🎮 Game Basics and Beginnings

### **The Tutorial**
The optional tutorial guides you through a dark cabin to teach the fundamentals of world interaction searching/equipping items, building basic defenses, and operating vehicles.

### **Character Creation and Starting Archetypes**
During character creation, you choose an archetype. Each features unique starting inventory items and skills.

**Examples** 

* Construction Worker
* Chef
* Thief
* Teacher
* Conspiracy Theorist
* Veteran


**Traits** 

You can select three additional skills and optional "challenge" traits, such as being *lactose intolerant* or *near-sighted*. These offer unique hurdles that create situations you wouldn't encounter otherwise.

### **Difficulty and Admin Tweaks**
The default difficulty ranges from **Basic to Impossible**, affecting seasons (Spring through Winter), loot availability, and zombie populations.

**Threat Levels**

You can adjust settings to include tougher zombies, larger hordes, or increased numbers of "runners." 

**Precision**

Use the "Headshots Only" mode to practice effective combat by forcing you to deliver the final killing blow to the head.

**Customization**

These settings are adjustable via `.ini` files or live in-game using the Admin menu or the in-game console (`~`). See the [Server Guide](vein-servers.md) for more information on the Admin menu and `.ini` file locations.

### **Starting Your Journey**
After deciding on a starting location, you will begin in a random house, likely in total darkness. 

**Phone (F)**

Press `F` to access your phone's flashlight. Note that phone batteries drain quickly; use it sparingly until you get your bearings. Find a light switch or open a door to let in natural light.

**Points of Interest (POIs)**

These are unique locations on the map that offer higher-tier loot. Improving your **Scavenger** skill helps you find better items, while **Lockpicking** and **Dismantling** are required for certain tasks.

**Navigation**

Without a cell phone or GPS, you cannot see your exact coordinates on a paper map alone.

---

<a name="inventory"></a>
## 🎒 Inventory and Equipment

### **Inventory Management**

#### **Sorting**

Use the tabs at the top to filter items by category.

#### **Favoriting (`*`)** 

Pins items to the top of your list.

#### **Locking (Padlock)**

Prevents items from being moved during bulk inventory transfers.

#### **Lighting (F)**

The default lighting toggle cycles through your highest-power devices **Headlamp** -> **Flashlight** -> **Cell Phone**.

#### **The Paper Doll**

The "Paper Doll" menu displays clothing and body armor. Each item has combat resistance and insulation ratings. Worn items are marked with a small square in the inventory list and can degrade or take damage over time.

#### **Equipping Items**

Items can be dragged to the hotbar (1-9) or your Paper Doll. You can reorder your hotbar by dragging and dropping items within the list.

---

<a name="classes"></a>
## 🗃️ Inventory Classes

![](/assets/logoweapons.png)

#### 🟥 **Weapons**

Many items not explicitly marked as weapons—such as hammers, mops, and whisks—can be used as alternatives. Metal pipes, baseball bats, and marshmallow spears are among the dozens of tools that function as blunt weapons. Firearms are effective for controlling zombies but will attract more to your area. Heavier melee weapons are more effective for stunning or knocking back enemies.

![](/assets/logoarmor.png)

#### 🟧 **Armor**

Vests, kneepads, and helmets can be found at POIs or looted from zombies. Armor increases your defensive stats but adds **Weight** and generates **Heat**.

![](/assets/logoclothing.png)

#### 🟦 **Clothing**

Gloves are vital for surviving the cold, preventing electric shocks during hotwiring, and are required for smelting to avoid burns. Raincoats and Hazmat suits are waterproof and will protect your electronics from water damage.

![](/assets/logoconsumables.png)

#### 🟩 **Consumables**

Hunger and Thirst are measured on a scale of `-100 to +100`. Nutritious food and water are vital. Overeating causes weight gain; the "sweet spot" is between -50 and +50. Books and comics reduce stress and improve mood. Alcohol and drugs are also available for "fun."

![](/assets/logomedical.png)

#### 🟪 **Medical**

Treat physical ailments like scratches, bites, and bruises to avoid infection or sickness. The treatment order is typically Sterilize -> Suture (for deep wounds) -> Bandage (cloth scraps can be used). Sleep speeds up the healing process.

![](/assets/logoammunition.png)

#### 🟨 **Ammunition**

Scavenge homes and businesses for rounds and magazines. **Warning** When swapping a locked mag in combat, the discarded mag will be marked as *Unlocked* in your inventory.

![](/assets/logomaterials.png)

#### 🟣 **Material**

Building requires raw materials like scrap, wood planks, screws, nails, and springs. You can also recover vehicle components like radios and tires.

![](/assets/logotools.png)

#### 🟦 **Tools**

Tools have four tiers **Basic, Advanced, Powered, and Hydraulic.** Crafting requires tools to be placed inside a workbench.

![](/assets/logospecial.png)

#### 🟦 **Special**

Includes keys, crafting schematics, and skill books to improve your character or provide access to containers and vehicles.

![](/assets/logojunk.png)

#### 🟫 **Other**

Items like cups and bowls are useful for carrying liquids. Salvaging mail parcels may yield tools or clothing.

![](/assets/logorecent.png)

#### 🟨 **Recent**

Provides quick access to the last several items acquired in your inventory.

---

<a name="building"></a>
## 🛠️ Base Building and Crafting

### **Building your first base**

#### **Utility Cabinet (UC)**

Required to build any base items via the **B Menu**.

#### **Workbenches** 

There are three tiers; higher tiers include all lower-tier recipes.

#### **Wall Building** 

There is no world grid. Walls pivot 22.5 degrees. Always build in one session to ensure panels interlock correctly; exiting the menu resets the "first" panel placement.

#### **Power/Water**

Connections are chained from the item to the source

**Examples**

* Lamp -> Electrical Panel -> Generator
* Washer -> Sink -> Blue Barrel

---

<a name="vehicles"></a>
## 🚗 Looting & Vehicles

#### **Capacity**

Vehicle trunks hold between 300 lbs and 3000 lbs.

#### **Examples** 

Cars/sedans, tractors, ambulances, and school buses.

#### ⚠️ **Physics Warning** 

In Early Access, do not stack items on roofs or beds; physics glitches during collisions can destroy them. 

#### ⚠️ **Hard Save** 

**\*** Always save manually before and after loading or unloading a vehicle.

#### ⚠️ **Logout Warning** 

Never log off while inside a vehicle or with items on it; they may launch into "orbit" upon reloading. 

#### * *See note [vein-servers.md](vein-servers.md) (2026-05-09)*

Some functionality is currently only available in version 0.24, experimental.

Other mitigations and fixes relating to the game's save states have been implemented for the community.

---

<a name="survival-tips"></a>
## ⚒️ Survival Tips

### ![](/assets/logoslaughtercolor.png)
**Slaughtering**
---

#### ![](/assets/logoskin.png)
**Skin**

Chances of receiving Leather

#### ![](/assets/logoguts.png)

**Gut**

Chances of receiving Organs

#### ![](/assets/logomeat.png)

**Butcher** 

Chances of receiving Meat

#### ![](/assets/logoblood.png)

**Bloodletting**

Use a syringe or pump into container for keeping blood.

---

![](/assets/logofarmingcolor.png)

### **Farming**

#### Requires
* garden plot
* soil
* seeds
* water
* light.

---

![](/assets/logoforaging.png)

### **Foraging**

Foraging description (0.24)

---

![](/assets/logoforging.png)

### **Forging**

Turn scrap into ingots. 

**ALWAYS WEAR GLOVES** to prevent burns.

---

![](/assets/logozombiehand.png)

### **Zombies**

Currently, there are three types of zombies roaming, resting in Vein 
* **Crawlers**
* **Walkers**
* **Runners** 

They are more likely to attack if you build large bases, create noise, or are visible from a distance.  

Keeping both yourself and the area you're keeping as a base, as clean as possible.

---

![](/assets/logowater.png)

**Water is Wet** 

Rain, sprinklers, and bodies of water will make you and your items wet.

Use raincoats or hazmat suits to protect electronics. Store electronic devices and batteries in storage before entering water to avoid damaging them.

---

