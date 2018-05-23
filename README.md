# Private Tracker Server Installation And Configuration Guide

## Client
* [Deluge](#deluge)
* Transmission

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
I hold that daemon management under Systemd is a better approach.
