# Private Tracker Server Installation And Configuration Guide
![](https://img.shields.io/badge/python-2.7-green.svg) ![](https://img.shields.io/badge/license-MIT-blue.svg) ![](https://img.shields.io/badge/docs-only-red.svg)
## Client
* [Deluge](#deluge)
  * [Install Latest Deluge on Ubuntu Server 18.04 x64](#install-latest-deluge-on-ubuntu-server-1804-x64)
  * [Daemon Management](#daemon-management)
  * [Log In](#log-in)
* [Transmission](#transmission)
  * [Install Latest Transmission on Ubuntu Server 18.04 x64](#install-latest-transmission-on-ubuntu-server-1804-x64)
  * [Configure the Transmission](#configure-the-transmission)
  * [Log In](#log-in-1)

### Deluge
What is Deluge? [Deluge](https://dev.deluge-torrent.org/wiki/Download) is a lightweight, Free Software, cross-platform BitTorrent client.
#### Install Latest Deluge on Ubuntu Server 18.04 x64
The latest release is version 1.3.15 . Check the release notes [here](https://dev.deluge-torrent.org/wiki/ReleaseNotes) before install it. You can install a daemon tool on a server and manage Deluge via deluge-webui which is a concise web UI for the browser. Try the command below to install it.
```
sudo apt install software-properties-common
sudo add-apt-repository ppa:deluge-team/ppa
sudo apt update
sudo apt install deluge-webui deluged
```
#### Daemon Management
Using `screen` to manage your daemons is a simple way. Maybe I do not advocate this.
```
sudo apt install screen
deluged
screen -S "deluge"
sudo deluge-web
screen -r deluge // switch
```
I hold that daemon management under Systemd is a better approach. For security it is best to run a service with a specific user and group. You can create one using the following command:
```
sudo adduser --system  --gecos "Deluge Service" --disabled-password --group --home /var/lib/deluge deluge
sudo adduser <username> deluge
```
Then create two files containing the following:
```
vim /etc/systemd/system/deluged.service
```
```
[Unit]
Description=Deluge Bittorrent Client Daemon
Documentation=man:deluged
After=network-online.target

[Service]
Type=simple
User=deluge
Group=deluge
UMask=007
ExecStart=/usr/bin/deluged -d
Restart=on-failure
# Time to wait before forcefully stopped.
TimeoutStopSec=300

[Install]
WantedBy=multi-user.target
```
```
vim /etc/systemd/system/deluge-web.service
```
```
[Unit]
Description=Deluge Bittorrent Client Web Interface
Documentation=man:deluge-web
After=network-online.target deluged.service
Wants=deluged.service

[Service]
Type=simple
User=deluge
Group=deluge
UMask=027
# This 5 second delay is necessary on some systems
# to ensure deluged has been fully started
ExecStartPre=/bin/sleep 5
ExecStart=/usr/bin/deluge-web
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
Now enable it to start up on boot, start the service and verify it is running:
```
sudo systemctl enable /etc/systemd/system/deluged.service
sudo systemctl start deluged
sudo systemctl status deluged

sudo systemctl enable /etc/systemd/system/deluge-web.service
sudo systemctl start deluge-web
sudo systemctl status deluge-web
```
#### Log In
Open your web browser and input this URL `<your_server's_ip:8112>` , you will be asked to enter a password which is by default set as `deluge` . After sign in, do not forget to change another password, then enjoy it.

### Transmission
What is Transmission? [Transmission](https://transmissionbt.com/) uses fewer resources than other clients. It has native Mac, GTK+ and Qt GUI clients and daemon ideal for servers support. All these can be remote controlled by Web and terminal clients. Transmission has the features you want from a BitTorrent client: encryption, a web interface, peer exchange, magnet links, DHT, µTP, UPnP and NAT-PMP port forwarding, webseed support, watch directories, tracker editing, global and per-torrent speed limits, and more.
#### Install Latest Transmission on Ubuntu Server 18.04 x64
Currently the version is 2.94. You can found the previous releases [here](https://github.com/transmission/transmission/releases). Just like Deluge, Transmission also has a transmission-daemon which to be deployed onto any server. Now, let's install it.
```
sudo apt update
sudo apt install transmission-daemon
sudo apt autoremove
```
The following additional packages will be installed: `libminiupnpc10` ` libnatpmp1` `transmission-cli` `transmission-common`. Since the daemon is starting, you can not modify the configuration immediately at all. What you have to do is stop it temporarily before the modification:
```
sudo service transmission-daemon stop
vim /var/lib/transmission-daemon/info/settings.json
```
#### Configure the Transmission
What's more, `/var/lib/transmission-daemon/info/settings.json` links to `/etc/transmission-daemon/settings.json`. You need to change the first one
exclusively. And [here](https://github.com/transmission/transmission/wiki/Editing-Configuration-Files#options) is an option list of configuration files which format is JSON. Let's take a look at what the default file is.
```
{
    "alt-speed-down": 50,
    "alt-speed-enabled": false,
    "alt-speed-time-begin": 540,
    "alt-speed-time-day": 127,
    "alt-speed-time-enabled": false,
    "alt-speed-time-end": 1020,
    "alt-speed-up": 50,
    "bind-address-ipv4": "0.0.0.0",
    "bind-address-ipv6": "::",
    "blocklist-enabled": false,
    "blocklist-url": "http://www.example.com/blocklist",
    "cache-size-mb": 4,
    "dht-enabled": true,
    "download-dir": "/var/lib/transmission-daemon/downloads",
    "download-limit": 100,
    "download-limit-enabled": 0,
    "download-queue-enabled": true,
    "download-queue-size": 5,
    "encryption": 1,
    "idle-seeding-limit": 30,
    "idle-seeding-limit-enabled": false,
    "incomplete-dir": "/var/lib/transmission-daemon/Downloads",
    "incomplete-dir-enabled": false,
    "lpd-enabled": false,
    "max-peers-global": 200,
    "message-level": 1,
    "peer-congestion-algorithm": "",
    "peer-id-ttl-hours": 6,
    "peer-limit-global": 200,
    "peer-limit-per-torrent": 50,
    "peer-port": 51413,
    "peer-port-random-high": 65535,
    "peer-port-random-low": 49152,
    "peer-port-random-on-start": false,
    "peer-socket-tos": "default",
    "pex-enabled": true,
    "port-forwarding-enabled": false,
    "preallocation": 1,
    "prefetch-enabled": true,
    "queue-stalled-enabled": true,
    "queue-stalled-minutes": 30,
    "ratio-limit": 2,
    "ratio-limit-enabled": false,
    "rename-partial-files": true,
    "rpc-authentication-required": true,
    "rpc-bind-address": "0.0.0.0",
    "rpc-enabled": true,
    "rpc-host-whitelist": "",
    "rpc-host-whitelist-enabled": true,
    "rpc-password": "pw",
    "rpc-port": 9091,
    "rpc-url": "/transmission/",
    "rpc-username": "transmission",
    "rpc-whitelist": "127.0.0.1",
    "rpc-whitelist-enabled": true,
    "scrape-paused-torrents-enabled": true,
    "script-torrent-done-enabled": false,
    "script-torrent-done-filename": "",
    "seed-queue-enabled": false,
    "seed-queue-size": 10,
    "speed-limit-down": 100,
    "speed-limit-down-enabled": false,
    "speed-limit-up": 100,
    "speed-limit-up-enabled": false,
    "start-added-torrents": true,
    "trash-original-torrent-files": false,
    "umask": 18,
    "upload-limit": 100,
    "upload-limit-enabled": 0,
    "upload-slots-per-torrent": 14,
    "utp-enabled": true
}
```
Edit for yourself and start the daemon right now.
```
sudo service transmission-daemon start
```
#### Log In
`http://your.domain.name:9091/transmission/web/ ` is what you want. The asked username and password are set by yourself. Type them in and begin downloading.
