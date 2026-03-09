***
# VEIN: Frequently Asked Questions & Server Guide

### Quick Navigation
* [Server/Client Configurations](#configurations)
* [File Locations](#locations)
* [Console Commands](#commands)
* [Troubleshooting](#troubleshooting)
* [Bug Reporting](#reporting)

---

<a name="configurations"></a>
## 💻 Server/Client Configurations and Console

### **Q:** How can I access the admin menu?
Pressing backslash (`\`) will bring up the admin menu.  
* This works on a `QWERTY` keyboard with a `US` keyboard layout.
* If (`\`) does not work, you may be required to use the `Insert` key.
* If neither work, you may need to manually map your `Admin Menu` bind in your `GameUserSettings.ini`.

### **Q:** Which configuration (`.ini`) files are required for VEIN?
There are four (4) files located in the `Saved` path of your game client/server installation.

**Server and Client Configurations:**
* `Engine.ini`
* `Game.ini`

**Client Configurations Only:**
* `GameUserSettings.ini`
* `Input.ini`

---

<a name="locations"></a>
## 📂 Configuration File Locations

### **Q:** Where are the (client) configuration files located?
* **Windows:** `..\steamapps\common\Vein\Vein\Saved\Config\Windows`
* **Linux:** `../steamapps/common/Vein\Vein\Saved\Config\Linux`

### **Q:** Where are my (server) configuration files located?
* **Windows:** `..\steamapps\common\Vein\Vein\Saved\Config\WindowsServer`
* **Linux:** `../steamapps/common/Vein\Vein\Saved\Config\LinuxServer`

### **Q:** Where are my `.log` files located?
* **Windows:** `..\steamapps\common\Vein\Vein\Saved\Logs\`
* **Linux:** `../steamapps/common/Vein\Vein\Saved\Logs/`

---

<a name="commands"></a>
## ⌨️ Useful Console Commands

* `ShowHud`: (Toggle) Photo mode. Removes item names and HUD entirely.
* `PrintAllVeinSettings`: Dumps all current game and engine variables (cvars) to the log.
* `Teleport`: Move to specific coordinates or players.
* `GiveItem [ItemName] [Amount]`: Add specific items to your inventory.
* `SetTime [Value]`: Change the world clock.
* `Fly`: (Toggle) Spectator-style movement for building or screenshots.

---

## 🌐 Server API & Remote Management

### **Q:** How do I enable and use the game server's HTTP API?
The API allows for real-time monitoring of server data (Time, Weather, Players).
* Enable the API in your `Engine.ini` under the `[/Script/Vein.VeinHTTPServer]` section.
* Set your desired port (default is `8089`).
* You can query data using tools like `curl` or build custom dashboards to visualize server status, character profiles, and weather (temperature/wind direction).

### **Q:** How can I send commands remotely (RCON)?
VEIN does not currently support RCON.
* Please refer to the `#vein-modding` channel on the official Discord for more information on administration tools.
* Using the `\` admin menu is the currently supported and recommended method for server management.

---

<a name="troubleshooting"></a>
## ⚠️ Common Troubleshooting

### **Q:** My server isn't appearing in the server browser. Why?
* **Port Forwarding:** Ensure the game port (`7777`) and query port (`27015`) are open on your router/firewall.
* **IP Binding:** Unless you have a specific reason not to, check that your `Engine.ini` is correctly bound to all interfaces using `DefaultBindAddress = 0.0.0.0`.
* **Version Mismatch:** Ensure both the server and your client are on the same branch (e.g., both on Experimental). 

### **Q:** The game crashes on startup or when loading a save.
* **Verify Integrity:** *Right-click* the game in `Steam > Properties > Installed Files > Verify Integrity of Game Files`.
* **Clear Config:** Temporarily move your `Saved/Config` folder to the desktop and restart to see if a corrupted `.ini` file is the cause.
* **Update Drivers:** Ensure your GPU drivers are up to date (Windows/Linux).

---

<a name="reporting"></a>
## 🐛 Reporting and Feedback

### **Q:** I have something I'd like to report. How do I do this?

#### **In-Game Feedback**
While in-game, press `Esc` to enter your menu and select **Feedback**. Use this for map bugs, floating textures, or immediate issues.

#### **Discord Reports**
Join the official VEIN Discord and create a ticket under `#vein-bug-reports`. 
* For crashes, flag the report with `[Crash!!]`.
* Always upload your `Vein.log` file from the `Saved/Logs` folder.

***
