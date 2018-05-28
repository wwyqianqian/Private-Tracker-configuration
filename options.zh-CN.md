### Original Options
>  https://github.com/transmission/transmission/wiki/Editing-Configuration-Files#options

#### Bandwidth
* alt-speed-enabled: Boolean (default = false, aka 'Turtle Mode')
Note: Clicking the "Turtle" in the gui when the scheduler is enabled, will only temporarily remove the scheduled limit until the next cycle.
* alt-speed-up: Number (KB/s, default = 50)
* alt-speed-down: Number (KB/s, default = 50)
* speed-limit-down: Number (KB/s, default = 100)
* speed-limit-down-enabled: Boolean (default = false)
* peed-limit-up: Number (KB/s, default = 100)
* speed-limit-up-enabled: Boolean (default = false)
* upload-slots-per-torrent: Number (default = 14)
#### Blocklists
* blocklist-url: String (default = http://www.example.com/blocklist)
* blocklist-enabled: Boolean (default = false)
#### Files and Locations
* download-dir: String (default = default locations)
* incomplete-dir: String (default = default locations) Directory to keep files in until torrent is complete.
* incomplete-dir-enabled: Boolean (default = false) When enabled, new torrents will download the files to incomplete-dir. When complete, the files will be moved to download-dir.
* preallocation: Number (0 = Off, 1 = Fast, 2 = Full (slower but reduces disk fragmentation), default = 1)
* rename-partial-files: Boolean (default = true) Postfix partially downloaded files with ".part".
* start-added-torrents: Boolean (default = true) Start torrents as soon as they are added.
* trash-original-torrent-files: Boolean (default = false) Delete torrents added from the watch directory.
* umask: Number (default = 18) Sets transmission's file mode creation mask. See the umask(2) manpage for more information. Users who want their saved torrents to be world-writable may want to set this value to 0. Bear in mind that the json markup language only accepts numbers in base 10, so the standard umask(2) octal notation "022" is written in settings.json as 18.
* watch-dir: String
* watch-dir-enabled: Boolean (default = false) Watch a directory for torrent files and add them to transmission.
* Note: When watch-dir-enabled is true, only the transmission-daemon, transmission-gtk, and transmission-qt applications will monitor watch-dir for new .torrent files and automatically load them.
#### Misc
* cache-size-mb: Size (default = 4), in megabytes, to allocate for Transmission's memory cache. The cache is used to help batch disk IO together, so increasing the cache size can be used to reduce the number of disk reads and writes. Default is 2 if configured with --enable-lightweight.
* dht-enabled: Boolean (default = true) Enable Distributed Hash Table (DHT).
* encryption: Number (0 = Prefer unencrypted connections, 1 = Prefer encrypted connections, 2 = Require encrypted connections; default = 1) Encryption preference. Encryption may help get around some ISP filtering, but at the cost of slightly higher CPU use.
* lazy-bitfield-enabled: Boolean (default = true) May help get around some ISP filtering. Vuze specification.
* lpd-enabled: Boolean (default = false) Enable Local Peer Discovery (LPD).
* message-level: Number (0 = None, 1 = Error, 2 = Info, 3 = Debug, default = 2) Set verbosity of transmission messages.
* pex-enabled: Boolean (default = true) Enable [http://en.wikipedia.org/wiki/Peer_exchange Peer Exchange (PEX)].
* prefetch-enabled: Boolean (default = true). When enabled, Transmission will hint to the OS which piece data it's about to read from disk in order to satisfy requests from peers. On Linux, this is done by passing POSIX_FADV_WILLNEED to posix_fadvise(). On OS X, this is done by passing F_RDADVISE to fcntl(). This defaults to false if configured with --enable-lightweight.
* scrape-paused-torrents-enabled: Boolean (default = true)
* script-torrent-done-enabled: Boolean (default = false) Run a script at torrent completion.
* script-torrent-done-filename: String (default = "") Path to script.
* utp-enabled: Boolean (default = true) Enable Micro Transport Protocol (µTP)
#### Peers
* bind-address-ipv4: String (default = "0.0.0.0") Where to listen for peer connections.
* bind-address-ipv6: String (default = "::") Where to listen for peer connections.
* peer-congestion-algorithm: String. This is documented on http://www.pps.jussieu.fr/~jch/software/bittorrent/tcp-congestion-control.html.
* peer-id-ttl-hours: Number (default = 6) Recycle the peer id used for public torrents after N hours of use.
* peer-limit-global: Number (default = 240)
* peer-limit-per-torrent: Number (default = 60)
* peer-socket-tos: String (default = "default") Set the Type-Of-Service (TOS) parameter for outgoing TCP packets. Possible values are "default", "lowcost", "throughput", "lowdelay" and "reliability". The value "lowcost" is recommended if you're using a smart router, and shouldn't harm in any case.
#### Peer Port
* peer-port: Number (default = 51413)
* peer-port-random-high: Number (default = 65535)
* peer-port-random-low: Number (default = 1024)
* peer-port-random-on-start: Boolean (default = false)
* port-forwarding-enabled: Boolean (default = true) Enable UPnP or NAT-PMP.
#### Queuing
* download-queue-enabled: Boolean (default = true) When true, Transmission will only download download-queue-size non-stalled torrents at once.
* download-queue-size: Number (default = 5) See download-queue-enabled.
* queue-stalled-enabled: Boolean (default = true) When true, torrents that have not shared data for queue-stalled-minutes are treated as 'stalled' and are not counted against the queue-download-size and seed-queue-size limits.
* queue-stalled-minutes: Number (default = 30) See queue-stalled-enabled.
* seed-queue-enabled: Boolean (default = false) When true. Transmission will only seed seed-queue-size non-stalled torrents at once.
* seed-queue-size: Number (default = 10) See seed-queue-enabled.
#### RPC
* rpc-authentication-required: Boolean (default = false)
* rpc-bind-address: String (default = "0.0.0.0") Where to listen for RPC connections
* rpc-enabled: Boolean (default = true)
* rpc-host-whitelist: String (Comma-delimited list of domain names. Wildcards allowed using '*'. Example: "*.foo.org,example.com", Default: "", Always allowed: "localhost", "localhost.", all the IP addresses. Added in v2.93)
* rpc-host-whitelist-enabled: Boolean (default = true. Added in v2.93)
* rpc-password: String
* rpc-port: Number (default = 9091)
* rpc-url: String (default = /transmission/. Added in v2.2)
* rpc-username: String
* rpc-whitelist: String (Comma-delimited list of IP addresses. Wildcards allowed using '*'. Example: "127.0.0.*,192.168.*.*", Default: "127.0.0.1")
* rpc-whitelist-enabled: Boolean (default = true)
#### Scheduling
* alt-speed-time-enabled: Boolean (default = false)
* Note: When enabled, this will toggle the alt-speed-enabled setting.
* alt-speed-time-begin: Number (default = 540, in minutes from midnight, 9am)
* alt-speed-time-end: Number (default = 1020, in minutes from midnight, 5pm)
* alt-speed-time-day: Number/bitfield (default = 127, all days)
  * Start with 0, then for each day you want the scheduler enabled, add:
    * Sunday: 1 (binary: 0000001)
    * Monday: 2 (binary: 0000010)
    * Tuesday: 4 (binary: 0000100)
    * Wednesday: 8 (binary: 0001000)
    * Thursday: 16 (binary: 0010000)
    * Friday: 32 (binary: 0100000)
    * Saturday: 64 (binary: 1000000)
  * Examples:
    * Weekdays: 62 (binary: 0111110)
    * Weekends: 65 (binary: 1000001)
    * All Days: 127 (binary: 1111111)
* idle-seeding-limit: Number (default = 30) Stop seeding after being idle for N minutes.
* idle-seeding-limit-enabled: Boolean (default = false)
* ratio-limit: Number (default = 2.0)
* ratio-limit-enabled: Boolean (default = false)
