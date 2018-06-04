### Original Options
>  https://github.com/transmission/transmission/wiki/Editing-Configuration-Files#options


#### Bandwidth
* alt-speed-enabled: 参数是布尔值，代表是否开启计划时段限速（默认为否，又被称作「海龟模式」）。注意：当日程表模式开启时，在 gui 界面点击海龟那个图标，会暂时移除预先定时限制，直到下一个循环开始。
* alt-speed-up: 计划时段限速上传最大值。数字（单位 KB/s, 默认 = 50）
* alt-speed-down: 计划时段限速下载最大值。数字（单位 KB/s, 默认 = 50）
* speed-limit-down: 全局下载最大速度限制。数字（单位 KB/s, 默认 = 100）
* speed-limit-down-enabled: 是否开启全局下载限速。布尔值（默认 = false）
* speed-limit-up: 全局上传最大速度限制。数字（单位 KB/s, 默认 = 100）
* speed-limit-up-enabled: 是否开启全局上传限速。布尔值（默认 = false）
* upload-slots-per-torrent: 每个种子的连接数。数字（默认 = 14）

#### Blocklists
* blocklist-url: 自定义黑名单链接。字符串（默认 = http://www.example.com/blocklist）
* blocklist-enabled: 是否开启黑名单。布尔值（默认 = false）

#### Files and Locations
* download-dir: 自定义存放完全完成下载种子的路径。字符串（默认 = `../var/lib/transmission-daemon/downloads`）
* incomplete-dir: 自定义存放下载未完成的文件的目录。字符串（默认 = `../var/lib/transmission-daemon/Downloads`）
* incomplete-dir-enabled: 是否允许自定义存放下载未完成的文件目录。布尔值（默认 = false）。当允许的时候，新的种子将暂时下载在 `incomplete-dir` 这个目录里面，下载完成后，会自动被移动到 `download-dir` 目录。
* preallocation: 磁盘空间预分配。数字（0 = 关闭，1 = 快速，2 = 完全（2 虽然慢，但是能减少磁盘碎片），默认 = 1）
* rename-partial-files: 是否重命名部分文件。布尔值（默认 = true）。把部分下载文件改成以 `.part` 结尾的后缀。
* start-added-torrents: 布尔值（默认 = true）。一旦添加 torrents 后是否马上开始上传/下载/做种。
* trash-original-torrent-files: 布尔值（默认 = false）。是否自动删除从监视目录添加的 torrents 。
* umask: 数字（默认 = 18）。设置 transmission 的文件权限掩码。参考[这篇](http://developer.apple.com/documentation/Darwin/Reference/ManPages/man2/umask.2.html) 。如果想设置最高权限，那么就填写 0 。请记住 JSON 只接受 10 进制数字，所以标准 umask(2) 八进制的 "022" 写入 `settings.json` 要转换为 18。以此类推。
* watch-dir: 自定义监视目录。
* watch-dir-enabled: 布尔值（默认 = false）。从这个监视目录寻找种子文件之后自动添加到 transmission 。<br/> 请注意：当 `watch-dir-enabled` 设置为 true 的时候，只有 `transmission-daemon`，`transmission-gtk`，和 `transmission-qt applications` 会监视这个目录来寻找新的 `.torrent` 文件，并且自动加载他们。

#### Misc
* cache-size-mb: 大小（默认 = 4）单位是 `megabytes`，用来分配内存缓存。缓存用于批量处理磁盘 IO ，所以提升这个数值可以减少磁盘频繁读写的次数。如果配置了 `--enable-lightweight` ，那么默认值就是 2 而不是 4。
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
