***
# VEIN: Frequently Asked Questions & Server Guide
  ![Vein, the game](header.jpg)
### Quick Navigation
* [Server/Client Configurations](#configurations)
* [File Locations](#locations)
* [Console Commands](#commands)
* [Troubleshooting](#troubleshooting)
* [Common Abbreviations](#commonabbreviations)
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

### **Q:** How do I run a console command on my multiplayer server?
* **Admin privledges:** You can access your multiplayer server's admin and console menu by first adding the `steam64id` of the player to the `Game.ini` file, into either the `AdminSteamIDs` or `SuperAdmin` values
* **Admin Menu vs Console:** You can access the console using the `~` developer options, but most commands will not work without first appending the `ServerExec` prefix to the command.  It is recommended that you use the game's `Admin Menu`, which can typically be accessed using the `\` or `Insert` keys.

`vein.AISpawner.SpawnCapMultiplierZombie=5` - as an example this would set your AI's zombie multiplier slider to 5x

This can also be adjusted manually by accessing the `Engine.ini` file within your server's file configuration location.

### **Q:** How do I use the television or projector?  How does the `URL` or `File` sources to work?

* Select the television/projector, then `Examine Connections` and add electricity from any electricity source such as a panel on the wall, a generator.
* **For URL:**
  * Select your source by changing it to `URL`, then click on `Select URL or file` and either type in your URL into the entry prompt, or you can copy and paste the link from a known URL with an existing `.mp4` extension.
  * Turn the television from the Off to the On position
  * Press the `Play` button near the top of your television/projector menu, or switch your source until you are able to select `URL`
* **For File:**
  *   * Select your source by changing it to `File`, then click on `Select URL or file`.  You will see a list of any file ending with an `.mp4` extension from the path your movie files are located in.  
  * Turn the television from the Off to the On position
  * Press the `Play` button near the top of your television/projector menu, or switch your source until you are able to select `File`

### **Q:** Where are my local movie files located, so that I can play them in the television/projector?
* Your game installation path on both the Windows or Linux client, will contain the location for the game's movie selection.
  * **Linux:** `../steamapps/common/Vein/Vein/Content/Movies/`
  * **Windows:** `..\steamapps\common\Vein\Vein\Content\Movies\`
* All files must end in either `.mp4`, `.webm`, `.mp3`
* Other formats may work such as `.mkv` and `.avi` but are currently unsupported/tested.

---

<a name="commonabbreviations"></a>
## ⚠️ Common Abbreviations and Terms

## **Q:** What does UC mean?

### **A:** UC is an abbreviation for the game's Utility Cabinet.  You build the UC from within your `B`uild menu within the game.  The UC is required to build other items. in your world.

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
