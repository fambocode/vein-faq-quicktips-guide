# Installing Vein Dedicated Server on Linux

Debian and Ubuntu instructions

## References

- <https://ramjet.notion.site/Initial-Setup-279f9ec29f17809c9ebce81e96ec48e7>
- <https://github.com/Radical-Egg/vein-dedicated-server>

---

## Linux Server Installation

Once your operating system is installed, you will need to install the server dependencies, create a new service user, and install the core Vein server files into that user's home path.

### Debian installation

At the time of writing, Debian 13 is the most up-to-date and supported version.

**Install dependencies**

```bash
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install -y steamcmd lib32gcc-s1 lib32stdc++6 libstdc++6 libgcc-s1 libc6 libcurl4 libssl3 libatomic1 libuuid1 libicu76 libasound2 libpulse0 zlib1g python3
```

### Ubuntu installation

At the time of writing, Ubuntu 24.04 is the most up-to-date and supported version.

**Install dependencies**

```bash
sudo add-apt-repository multiverse
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install -y steamcmd lib32gcc-s1 lib32stdc++6 libstdc++6 libgcc-s1 libc6 libcurl4t64 libssl3t64 libatomic1 libuuid1 t64 libasound2t64 libpulse0 zlib1g python3
```

---

## Vein Server Configuration and Setup

When you have configured your Linux server, you can choose to set up the server under the active Vein/service user, or under root if the installer permits it.

### Create a non-root user

We want to make sure none of the services are running as root.

Logged in as the root user, add a new user to the server:

```bash
sudo useradd -m -s /bin/bash vein
sudo -iu vein
```

### Create game server folders and set up steamcmd

First, create the server folder under the user's home directory. We will also create a folder for Vein under the user's `.config` path, as previous Vein versions have used it.

```bash
mkdir -p ~/server ~/.config/Epic/Vein
steamcmd +login anonymous +quit
steamcmd +force_install_dir /home/vein/server +login anonymous +app_update 2131400 validate +quit
```

### Confirm game server and files

Now we need to verify that the game was installed correctly and that all your files are in their correct locations.

```bash
ls -lsa ~/server/Vein
```

You should see a folder structure and several files, including the `Saved/Config` path where the server's `Engine.ini` and `Game.ini` are stored.

### Optional: Link steamclient.so to the Vein installation path

The official Ramjet documentation notes that we need to find `steamclient.so` and link it into the Vein folder, in the correct location.

```bash
find ~ /usr -name steamclient.so 2>/dev/null
```

You may find one or two files: 32-bit and 64-bit versions, located in two separate locations. Typically the folder is indicated as `linux64`, e.g.:

```text
~/.steam/steam/steamcmd/linux64/steamclient.so
```

We need to link this file into the Vein directory.

First, verify that the directory exists:

```bash
ls -lsa ~/server/Vein/Binaries/Linux
```

If it does not exist, create it:

```bash
mkdir -p ~/server/Vein/Binaries/Linux
```

Now link the Steam client into the required path:

```bash
ln -sf ~/.steam/steam/steamcmd/linux64/steamclient.so ~/server/Vein/Binaries/Linux/steamclient.so
```

### Optional: Opening your VM's firewall

You may or may not have `ufw` or another firewall installed. The following instructions assume you are only running one server, using Game Port `7777` and Query Port `27015`.

Both ports are required for the server to display correctly and for clients to connect through the server browser.

| Firewall Rule   | ufw                              | firewalld                                           |
| --------------- | -------------------------------- | --------------------------------------------------- |
| Allow Game Port | `sudo ufw allow 7777/udp`        | `sudo firewall-cmd --permanent --add-port=7777/udp` |
| Allow Query Port| `sudo ufw allow 27015/udp`       | `sudo firewall-cmd --permanent --add-port=27015/udp`|
| Reload Firewall | N/A                              | `sudo firewall-cmd --reload`                        |

You will also need to ensure that your router's firewall ports are open and forwarding correctly to your server. There are several online guides on how to do this, and you can find help on the official Discord server.

---

## Starting the Server

Make sure your server can start before delving too deeply into configuration. Do this by changing into the Vein server directory and running the script file:

```bash
cd ~/server
chmod +x VeinServer.sh
./VeinServer.sh
```

## Stopping and Configuring the Vein Server

Once the server has launched and is running, shut it down so you can access the files it generated during installation.

Press `Ctrl+C` to close and shut down the server.

The config files are `Game.ini` and `Engine.ini`. On Linux they live under a `Saved/Config/LinuxServer/` directory. Previous builds left the saved game and server files under the user's `.config` folder, but this has since been resolved. The files should only exist in one location.

Find the `LinuxServer` folder within your home path:

```bash
find ~ -type d -name LinuxServer
```

---

## Optional/Recommended: Running Vein as a service

Before launching your server again, consider running your instance as a service.

This is easily done by creating a `vein.service` file in the correct location and enabling the service within your session.

Here is an example `vein.service` file:

```ini
[Unit]
Description=VEIN Dedicated Server
After=network-online.target
Wants=network-online.target

[Service]
User=vein
Group=vein
WorkingDirectory=/home/vein/server
Environment=HOME=/home/vein
ExecStartPre=/usr/games/steamcmd +force_install_dir /home/vein/server +login anonymous +app_update 2131400 validate +quit
ExecStart=/home/vein/server/VeinServer.sh
Restart=on-failure
RestartSec=10
TimeoutStartSec=600

[Install]
WantedBy=multi-user.target
```

> **Note on service restarts:**
> The steamcmd executable may be located somewhere other than `/usr/games/steamcmd`.
> The `ExecStartPre` line runs on every service restart. You will need to verify that this is the correct path for the steamcmd executable, or the service will fail.

**Enable the Vein service**

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now vein
journalctl -u vein -f
```

> **Tip:**
> If you run into issues where steamcmd is not found, steam may not have been added to the system's `PATH` environment variable. You can add a line to your service file so the various steamcmd locations are found:
>
> ```ini
> [Service]
> Environment=PATH=/usr/local/bin:/usr/bin:/bin:/usr/games
> ```

---

## Optional: Configure a robust Vein script, based on Egg's image

Giving credit where it's due, the work on Egg's unofficial image and scripts is what has led to several working servers. These are additional steps you can take to configure a more robust script, based on Egg's own entrypoint script and image.

Create a new file at `/home/vein/start-vein.sh` and add the following content:

```bash
#!/usr/bin/env bash
set -euo pipefail
VEIN_APP_ID="${VEIN_APP_ID:-2131400}"
VEIN_INSTALL_DIR="${VEIN_INSTALL_DIR:-$HOME/server}"
VEIN_BINARY="${VEIN_INSTALL_DIR}/VeinServer.sh"
VEIN_SERVER_AUTO_UPDATE="${VEIN_SERVER_AUTO_UPDATE:-true}"
VEIN_QUERY_PORT="${VEIN_QUERY_PORT:-27015}"
VEIN_GAME_PORT="${VEIN_GAME_PORT:-7777}"
VEIN_EXTRA_ARGS="${VEIN_EXTRA_ARGS:-}"
VEIN_SERVER_USE_BETA="${VEIN_SERVER_USE_BETA:-false}"
VEIN_SERVER_BETA_BRANCH="${VEIN_SERVER_BETA_BRANCH:-experimental}"
VEIN_SERVER_VALIDATE_INSTALL="${VEIN_SERVER_VALIDATE_INSTALL:-false}"
STEAM_HOME="${STEAM_HOME:-$HOME/.local/share/Steam}"
MANIFEST="${VEIN_INSTALL_DIR}/steamapps/appmanifest_${VEIN_APP_ID}.acf"

INSTALL_ARGS=()
[[ "$VEIN_SERVER_USE_BETA" == "true" ]] && INSTALL_ARGS+=(-beta "$VEIN_SERVER_BETA_BRANCH")
if [[ ! -f "$VEIN_BINARY" || "$VEIN_SERVER_VALIDATE_INSTALL" == "true" ]]; then
  INSTALL_ARGS+=(validate)
fi

steamcmd_install() {
  steamcmd +force_install_dir "$VEIN_INSTALL_DIR" +login anonymous \
    +app_update "$VEIN_APP_ID" "${INSTALL_ARGS[@]}" +quit
}

update_server() {
  local log; log="$(mktemp)"
  if steamcmd_install 2>&1 | tee "$log"; then rm -f "$log"; return 0; fi
  if grep -Fq "Error! App '${VEIN_APP_ID}' state is 0x6 after update job" "$log"; then
    echo "Got 0x6, removing stale manifest and retrying once..."
    rm -f "$MANIFEST"
    steamcmd_install && { rm -f "$log"; return 0; }
  fi
  rm -f "$log"; return 1
}

if [[ ! -f "$VEIN_BINARY" || "$VEIN_SERVER_AUTO_UPDATE" == "true" ]]; then
  update_server
fi

mkdir -p "${VEIN_INSTALL_DIR}/Vein/Binaries/Linux"
ln -sf "${STEAM_HOME}/steamcmd/linux64/steamclient.so" \
       "${VEIN_INSTALL_DIR}/Vein/Binaries/Linux/steamclient.so"

echo "Starting Vein server..."
# shellcheck disable=SC2086
exec "$VEIN_BINARY" -log -QueryPort="$VEIN_QUERY_PORT" -Port="$VEIN_GAME_PORT" $VEIN_EXTRA_ARGS
```

Make the script executable:

```bash
chmod +x /home/vein/start-vein.sh
```

Verify that `steamclient.so` exists in the expected location:

```bash
ls ~/.local/share/Steam/steamcmd/linux64/steamclient.so
```

Run the script:

```bash
~/start-vein.sh
```

Close your server with `Ctrl+C`, then follow the example procedure above to run your Vein script as a system service.

---

## Edit Your Server Configuration Files

Once your server is configured and offline, you can edit the two main configuration files, `Game.ini` and `Engine.ini`.

Find your `Game.ini` file first, and configure your server launch parameters:

```bash
find ~ -name Game.ini -path "*LinuxServer*"
```

## Updating Your Server Configuration Files

You can restart your server manually and allow it to update by restarting the service:

```bash
sudo systemctl restart vein
```
