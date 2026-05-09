# 💻 VEIN: Server Guide & Technical FAQ

![Vein, the game](assets/header.jpg)

[**Home**](index.md) | [**Survival Guide**](vein-client.md) | [**Server Guide**](vein-servers.md) | [**Media List**](public-domain-movies.md)

---

## Table of Contents
1. [Configurations and Admin Access](#configurations)
2. [File Locations](#locations)
3. [Console Commands](#commands)
4. [Server API & Remote Management](#api)
5. [In-Game Multimedia](#multimedia)
6. [Troubleshooting](#troubleshooting)

---

<a name="configurations"></a>
## 💻 Configurations and Admin Access

### **Q: How do I access the Admin Menu?**

#### Press the backslash key (`\`) to bring up the admin menu.
* This works on standard `QWERTY` keyboards with a `US` layout.
* If (`\`) does not work, you may need to use the `Insert` key instead.
* Certain international layouts are known to work using the `§` key.
* If none of these work, you may need to manually map your `Admin Menu` bind within `GameUserSettings.ini`.

### **Q: Which configuration (.ini) files are required?**

#### There are four essential files located in the `Saved` path of your installation.

Not all `.ini` files are used by both the server and the client.  Some are reserved for client use.

#### **Server & Client `.ini` files:**

| FileName | Server | Client |
| :--- | :--- | :--- |
| `Engine.ini` | Yes | Yes |
| `Game.ini` | Yes | Yes |
| `GameUserSettings.ini` | No | Yes |
| `Input.ini` | No | Yes |

---

<a name="locations"></a>
## 📂 File Locations

| Type | Windows Path | Linux Path |
| :--- | :--- | :--- |
| **Client Config** | `..\Saved\Config\Windows` | `../Saved/Config/Linux` |
| **Server Config** | `..\Saved\Config\WindowsServer` | `../Saved/Config/LinuxServer` |
| **Logs** | `..\Saved\Logs\` | `../Saved/Logs/` |
| **Movies** | `..\Content\Movies\` | `../Content/Movies/` |


---

<a name="commands"></a>
## ⌨️ Useful Console Commands

### Access the console using the tilde key (`~`). In multiplayer, prefix these commands with `ServerExec`. 

To enable these, you must add the `steam64id` of the player to `Game.ini` under the `AdminSteamIDs` or `SuperAdmin` sections.

* **`ShowHud`**: (Toggle) Enables Photo Mode by removing item names and the HUD entirely.
* **`PrintAllVeinSettings`**: Dumps all current game and engine variables (cvars) to the log file.
* **`Teleport`**: Move instantly to specific coordinates or other players.
* **`GiveItem [ItemName] [Amount]`**: Adds specific items directly to your inventory.
* **`SetTime [Value]`**: Adjusts the world clock.
* **`Fly`**: (Toggle) Enables spectator-style movement for easier building or cinematic screenshots.

### **Console Command Example(s):** 

`ServerExec vein.AISpawner.SpawnCapMultiplierZombie=5`

---

<a name="api"></a>
## 🌐 Server API & Remote Management

### **HTTP API** 

This can be enabled in `Engine.ini` under the `[/Script/Vein.VeinHTTPServer]` section. The default port is `8080`.
* The API allows for real-time monitoring of server data such as Time, Weather, and Player lists.
* You can query this data using `curl` or custom dashboards to visualize live server status.

### **Example Port Configuration:**

#### To change the port from `8080` to `8089`, use the following structure in your `Engine.ini`:

```ini
[/Script/Vein.VeinHTTPServer]
bEnabled=True
Port=8089
DefaultBindAddress=0.0.0.0
```
### HTTP API endpoints

Multiple endpoints are available on the HTTP API that a VEIN dedicated server can run.

* `/players`
* `/characters`
* `/status`
* `/weather`
* `/time`

#### *Note (2026-05-09): Plans for `/Save` and `/SaveExit` endpoint functionality are currently in version 0.24 experimental.*

### **RCON**

VEIN does not currently support RCON. For alternative administration tools, please refer to the `#vein-modding` channel on the official Discord server.

---

<a name="multimedia"></a>
## 📺 In-Game Multimedia & Security

### Television and Projector (.mp4 Playback)
First, select the device, then use `Examine Connections` to add electricity from a valid power source.

#### **Via URL:**

* Set the source to `URL`. Click `Select URL or file` and paste a direct link ending in `.mp4`.
* Set the TV to the **On** position and press **Play**.

#### **Via Local File:**
* Set the source to `File`. Select from the list of `.mp4` files located in your Movies folder.
* Set the TV to the **On** position and press **Play**.

#### **Technical Notes & Limitations:**

* Not every `.mp4` is compatible due to varying codecs. Linux users may require Proton for stable playback.

### **Multiplayer:**

All players must have identical `.mp4` files in their local `Movies` directory to view the video. Timings may not be perfectly synced between clients.

#### **Remote Viewing:**

All players must have the "Remote Viewing" option enabled in their game settings to see streams from other players.

### Security Cameras

Adding electricity to both the camera and the television **is required**.

1. **Camera:** Use `Examine Connections` to connect it to a power source.
2. **TV:** Use `Examine Connections` to connect it to a power source, then set the source to `Camera`.
3. **Linking:** At the bottom of the TV menu, select `Add Camera` and link it to your installed camera hardware.
4. **Range:** Cameras have a short default range; this can be adjusted within your `Engine.ini`.
5. **Cycling:** Use the `Next Camera` and `Previous Camera` options to switch between multiple feeds on one screen.

---

<a name="troubleshooting"></a>
## ⚠️ Troubleshooting & FAQ

### **Server Visibility:** 

* Ensure you have opened ports `7777` (Game) and `27015` (Query) on your routing equipment, the server host device and any other firewall requiring your local or remote connections.


* Confirm `DefaultBindAddress = 0.0.0.0` is set in your `Engine.ini`.

### **What is a UC?** 

The **Utility Cabinet** (UC) is the essential component required for all base construction via the `B` menu.

### **Reporting Issues:** 

Use `Esc` -> **Feedback and Bugs** in-game to report map-related issues. For technical crashes, visit the `#vein-bug-reports` Discord channel and attach your `Vein.log`.

![](/assets/feedback-example.png)
---