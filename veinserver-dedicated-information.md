# How to Install a Vein Server

How to install and host your own dedicated Vein server

---
## References

A new guide on creating a dedicated Vein server on Linux Debian and Ubuntu

https://github.com/fambocode/vein-faq-quicktips-guide/blob/main/veinserver-dedicated-guide-linux.md

The source material for this markdown guide

https://vein.wiki.gg/wiki/Vein_Dedicated_Server_Information

## Disclaimer

This guide was revised and reworked for releases 0.023 through 0.025, and tested within the Discord community. The dedicated server experience has improved dramatically through 2026, and we are expecting a change in the game's networking within one of the newer planned release cycles.

## Prerequisites

Though the Windows server installations have been tested on Windows Server and client devices, the DirectX and VC_redist executables within the `_CommonRedist` folder of the server installation may be required on certain builds of the Windows operating system. Specifically, the Vein server in a Windows environment requires both in order to function correctly.

---

## Hardware Requirements

Though more is better, your system's performance will depend heavily on a few factors. Generally speaking, the more CPU cores you have, and the more and faster RAM you have, the more stable your server will behave.

Your drive speed also directly impacts your overall performance, so be mindful of slower spinning HDD drives. SSD and NVMe drives are recommended for the server installation.

### CPU/Processors

Vein as a server does not require a lot of CPU power, but it can have an impact during various dynamic events happening in the game world as players are building and moving around. The I/O rate (see [Drives](#drives)) at which your CPU and drive can read and write has a very strong impact on Vein's overall performance for clients.

#### Architecture

Both your operating system and system hardware must support 64-bit, as the `VeinServer` binaries/executables will not run or correctly install in a 32-bit environment.

#### Core Count

Vein seems to favor 1-4 cores during its heavier loads. As of version 0.025, the CPU will often spike when dealing with clients being further apart on the map and all actively working on their various tasks. As of this writing, the server will have a varying degree of impact on the CPU over its uptime, and shortly after a server restart/update.

### RAM

RAM usage on a Vein server can be expected to change over time. The general guidelines have been suggested through the community and are not accurate to your own server hardware and performance. As the game gains development, it is expected that the total amount of RAM required for servers and clients will be different than is recommended today.

#### Format and Speed

The type of RAM used in a Vein server can definitely impact the overall performance, but consumer-grade DDR4 and DDR5 have proven to do well under pressure.

#### Amount

You will need, at a very minimum, 8 GB of available memory to run Vein as a server. It is recommended that you dedicate the system to Vein, as it will require more resources than most game servers over its duration and server uptime.

- Once a server reaches 3 players, 16 GB of RAM is recommended.
- Once it reaches 4 players or more, the server may increase its memory requirements quickly, and thus 32 GB is recommended for 4+ players.

### Drives

#### Format and Speed

All efforts should be made to avoid serving either the client or server from an HDD. The server will suffer desync and stuttering issues when it has trouble reading and writing (I/O) to the drive(s).

A single SSD or NVMe drive will work. Drive pools running the servers should also avoid running off of an HDD.

#### Amount

You will need between 35 and 60 GB of available drive space to run and update your Vein server.

---

## Network

The Vein server executable runs as a service that defaults to two ports. One is named the Query Port, the other the Game Port.

Vein as a dedicated instance also offers admins access to an API. This can be enabled within the configuration files for Vein.

Server administrators are expected to know and understand how to manage incoming and outgoing network traffic in order to proceed. Please ask for more advice in the Discord. The network traffic and port configuration guide will be very limited.

### Ports

The following table shows the ports required for a Vein server to work correctly.

| Port    | Port Type | Purpose    |
| ------- | --------- | ---------- |
| `7777`  | UDP       | Game port  |
| `27015` | UDP       | Query port |
| `8080`  | TCP       | API port   |

### Your Public IP

Your public IP, as well as the type of routing and network equipment you are running, all have an impact on whether you will see connections to your server. Even if you do everything correctly, you still risk having a provider who blocks your router and network from hosting anything.

You may also have a provider who has a limited number of public IP addresses to hand to you, their client. If this is the case, your provider will hand your network and routing equipment a private IP address, otherwise known as a CGNAT network. Your options for providing clients access to your own game server are strictly limited by the public IP provider's network and infrastructure.

### Multiple Servers

While a single server is supported using ports `7777` and `27015`, other port numbers can be used within your network environment, as long as the port mapping rules are respected across the network infrastructure. While you are planning your port configurations, you will need to ensure that the port numbers in the provided configuration (`.ini`) files are identical to the ports being forwarded through your NAT/routing table.

The server information that is sent to the server browser identifies your server based on the information in your `.ini` files. It does **NOT** only reflect what you have provided in your NAT table.

### Local Network

When hosting on your own network, you will need to use the Direct Connect option within your Vein client. You will need to know the Vein server's private IPv4 address and port, such as `192.168.0.2:7777`.

If you are hosting the server on the same device as the client, you will need to connect with your localhost IP address at `127.0.0.1:7777` in order to establish a truly local connection.

---

## Example Network Scenarios

The following is a non-exhaustive list of scenarios covering the more common self-hosted/dedicated server and network environments.

### Scenario 1: Single Server

I cannot use ports 7777 and 27015 (for example, they are already in use or blocked) and only require one server on a single public IP address.

My server has a Game Port of 30000 and a Query Port of 30010.

| Game.ini location and key-pair                   | Local and Host Firewall(s) | NAT/Port Forward Entry         |
| ------------------------------------------------ | -------------------------- | ------------------------------ |
| `[URL]`<br>`Port=30000`                         | Open port 30000 UDP        | `LAN:30000<>WAN:30000/udp`     |
| `[OnlineSubsystemSteam]`<br>`GameServerQueryPort=30010` | Open port 30010 UDP      | `LAN:30010<>WAN:30010/udp`     |

### Scenario 2: Two Servers

I am not limited in using any port, but I'd like to host several servers from a single public IP address.

One server has a Game Port of 7777 and a Query Port of 27015.

My second server has a Game Port of 7778 and a Query Port of 27016.

| Game.ini location and key-pair                     | Local and Host Firewall(s) | NAT/Port Forward Entry     |
| -------------------------------------------------- | -------------------------- | -------------------------- |
| `[URL]`<br>`Port=7777`                                  | Open port 7777 UDP         | `LAN:7777<>WAN:7777/udp`   |
| `[OnlineSubsystemSteam]`<br>`GameServerQueryPort=27015` | Open port 27015 UDP        | `LAN:27015<>WAN:27015/udp` |
| `[URL]<br>Port=7778`                                  | Open port 7778 UDP         | `LAN:7778<>WAN:7778/udp`   |
| `[OnlineSubsystemSteam]`<br>`GameServerQueryPort=27016` | Open port 27016 UDP        | `LAN:27016<>WAN:27016/udp` |

### Scenario 3: CGNAT/Private IP Server

My provider limits my router to an IP address similar to `192.168.4.5`/`172.16.1.2` and I cannot host from my network.

I have one server with a Game Port of 7777 and a Query Port of 27015.

> **Note:** While this is currently unavailable, there may be other mitigations and network changes that will allow servers to tunnel directly without a NAT entry. For further reading and study, please refer to Cloudflare or Tailscale for free access to tunneling your services securely.

### Scenario 4: Local Network Only Server

I'd like to host locally on my network. I don't plan on having anyone from the outside connect.

I have one server with a Game Port of 7777 and a Query Port of 27015.

| Game.ini location and key-pair                     | Local and Host Firewall(s) | NAT/Port Forward Entry |
| -------------------------------------------------- | -------------------------- | ---------------------- |
| `[URL]`<br>`Port=7777`                                  | Open port 7777 UDP         | N/A                    |
| `[OnlineSubsystemSteam]`<br>`GameServerQueryPort=27015` | Open port 27015 UDP        | N/A                    |

### Scenario 5: Local Client and Server Only

I'd like to host locally on the same device I play Vein on. I don't plan on having anyone connect from the outside.

I have one server with a Game Port of 7777 and a Query Port of 27015.

| Game.ini location and key-pair                     | Local and Host Firewall(s) | NAT/Port Forward Entry |
| -------------------------------------------------- | -------------------------- | ---------------------- |
| `[URL]`<br>`Port=7777`                                  | N/A                        | N/A                    |
| `[OnlineSubsystemSteam]`<br>`GameServerQueryPort=27015` | N/A                        | N/A                    |

### Scenario 6: I Dunno

This seems complicated.

Can I just pay someone?

| Game.ini location and key-pair         | Local and Host Firewall(s)    | NAT/Port Forward Entry |
| -------------------------------------- | ----------------------------- | ---------------------- |
| Game server provider surely knows.     | Ask them; isn't fire bad?     | Yeah, those!           |

---

## Virtual Machines\*\* and Docker\*\*

When working with virtual machines, the machine type has an impact on whether the server will perform well. The default virtual experience provided by a hypervisor may not be enough to launch Vein and will result in possible errors or crashes. The stdout and log output for Vein will mention whether you have the correct processor and architecture to launch it as an executable service.

The following is an example of EFI virtual hardware confirmed working with Vein:

| Server System Information | Physical                      | Virtual                              |
| ------------------------- | ----------------------------- | ------------------------------------ |
| Hypervisor/O.S            | Proxmox (Debian 12)           | Windows\*/Linux/Docker\*\*           |
| Machine arch.             | Intel x64                     | ovmf/uefi, q35, virtio               |
| CPU                       | 1 socket, 6 cores, 12 threads (i7-8700K)   | 2 sockets, 3 cores (x86-64-v2-AES)   |
| RAM                       | 64 GB DDR4                    | 40 GB                                |
| Disk                      | 1 x 128 GB SSD                | 1 x 100 GB VirtIO SCSI single        |
| Network                   | 2.5 Gbps ethernet             | 1 x 1 Gbps VirtIO paravirtualized    |

\* Windows client and server require activation. Though a Windows device in a grace period should not impact the server's performance, it can impact which features you might not have access to once the server's activation expires. Windows Server is recommended for your virtual environment hosting services.

\*\* Linux dependencies for steamcmd require quite a lot of work to keep updated without breaking other dependencies.  Docker Desktop can be used but is not supported due to its overarching complexity in handling DNS and networking traffic over Hyper-V and WSL/Docker.
