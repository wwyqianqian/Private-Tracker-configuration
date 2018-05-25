# Private Tracker Server Installation And Configuration Guide
![](https://img.shields.io/badge/python-2.7-green.svg) ![](https://img.shields.io/badge/license-MIT-blue.svg) ![](https://img.shields.io/badge/docs-only-red.svg)
## Client
* [Deluge](#deluge)
  * [Install Latest Deluge on Ubuntu Server 18.04 x64](#install-latest-deluge-on-ubuntu-server-1804-x64)
  * [Daemon Management](#daemon-management)
  * [Log In](#log-in)
* [Transmission](#transmission)

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
