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
* dht-enabled: 是否开启分散式哈希表 `Distributed Hash Table` 。布尔值（默认 = true）。 **如果下载 pt 的话，要改成不允许。**
* encryption: 是否选择加密。数值（0 = 首选不加密的连接，1 = 首选加密连接，2 = 只连接加密的连接；默认 = 1）。加密可能有助于解决一些 `ISP 过滤（ISP filtering）`（防止运营商或者 ISP 封杀 BT） 问题，但代价是 CPU 消耗略高。
* lazy-bitfield-enabled: 布尔值（默认 = true）。可能有助于解决一些 `ISP 过滤` 问题。是 Vuze（一种 BitTorrent 客户端）的规范。
* lpd-enabled: 布尔值（默认 = false）。是否开启 `本地节点侦测 Local Peer Discovery` 。 **pt 下载需要关掉。**
* message-level: 消息等级。数值（0 = 无，1 = 错误，2 = 详细，3 = 排错，默认 = 2）。设置客户端显示消息细节程度。
* pex-enabled: 布尔值（默认 = true）。[什么是 Peer Exchange 节点交换](http://en.wikipedia.org/wiki/Peer_exchange) 。 **pt 下载需要关闭。**
* prefetch-enabled: 预取模式，布尔值（默认 = true）。当允许时，Transmission 要告知操作系统哪部分数据要从磁盘读取，这样能达到peer的要求。Linux上，是通过将 `POSIX_FADV_WILLNEED` 传递给 `posix_fadvise()` 来完成的。在 Mac OS 上，这是通过将 `F_RDADVISE` 传递给 `fcntl()` 来完成的。如果有 `--enable-lightweight` 配置，则此默认值为false。
* scrape-paused-torrents-enabled: 布尔值（默认 = true）。
* script-torrent-done-enabled: 布尔值（默认 = false）。在 torrent 结束时是否运行脚本。
* script-torrent-done-filename: 字符串（default = ""）这里写入脚本的路径。
* utp-enabled: 布尔值（默认 = true）。是否允许 [Micro Transport Protocol (µTP)](https://zh.wikipedia.org/zh-cn/Micro_Transport_Protocol) 。注：Transmission从 2.30 版开始支持 µTP。

#### Peers
* bind-address-ipv4: 绑定 v4 地址，字符串（默认 = "0.0.0.0"）。监听 peer 连接用。
* bind-address-ipv6: 绑定 v6 地址，字符串（默认 = "0.0.0.0"）。监听 peer 连接用。
* peer-congestion-algorithm: tcp 拥塞控制，字符串。这里是文档：http://www.pps.jussieu.fr/~jch/software/bittorrent/tcp-congestion-control.html 。如果想使用 TCP-LP，请这里填写 `"lp"`。
* peer-id-ttl-hours: 数字 N（默认值= 6）。在使用 N 小时后，回收已经发布种子的 peer ID。
* peer-limit-global: 数字（默认 = 240）。全局 peer 数目限制。是用户上限。
* peer-limit-per-torrent: 数字（默认 = 60）。每个种子 peer 数目限制。
* peer-socket-tos: 字符串（默认 = "default"）。为发出的 TCP 数据包设置服务类型（Type-Of-Service:TOS）参数。这里可选择的填写是`“default”`（默认），`“lowcost”`（低耗），`“throughput”`（吞吐量），`“lowdelay”`（低延迟）和`“reliability”`（可靠性）。如果使用的是智能路由器，建议使用`“lowcost”`值，这样不应在任何情况下造成损害。

#### Peer Port
* peer-port: 数值（默认 = 51413）传入端口号。
* peer-port-random-high: 数值（默认 = 65535）随机端口号上限。
* peer-port-random-low: 数值（默认 = 1024）随机端口号下限。
* peer-port-random-on-start: 布尔值（默认 = false）。是否开启随机端口号。
* port-forwarding-enabled: 布尔值（默认 = true）。是否开启 UPnP 或者 NAT-PMP。

#### Queuing
* download-queue-enabled: 布尔值（默认 = true）。当设置为 true 时，Transmission 将会只下载当前队列里面未停滞的种子。
* download-queue-size: 数值（默认 = 5）下载队列大小限制。
* queue-stalled-enabled: 布尔值（默认 = true）。如果为 true，则时间不够 `queue-stalled-minutes` 分钟的种子将被视为“stalled”，并且不会计入 `queue-download-size ` 和 `seed-queue-size` 限制。
* queue-stalled-minutes: 数值（default = 30）。队列停滞分钟数目。
* seed-queue-enabled: 布尔值（默认 = false）当为 true 时，Transmission 会只立即做种 `seed-queue-size` 未停滞的种子。
* seed-queue-size: 数值（默认 = 10）。

#### RPC(Remote Procedure Call 远程过程调用)
* rpc-authentication-required: 布尔值（默认 = false）是否需要 RPC 验证。
* rpc-bind-address: 字符串（默认 = "0.0.0.0"）监听 RPC 连接地址。
* rpc-enabled: 布尔值（默认 = true）。是否开启 RPC。
* rpc-host-whitelist: 字符串（以逗号分隔的域名列表。允许使用 `'*'` 的通配符。例如：`“* .foo.org, example.com”`，默认值：“”，始终允许：“localhost”，“localhost.”，所有IP地址。在 2.93 版本中添加）。
* rpc-host-whitelist-enabled: 布尔值（默认 = true。在 2.93 版本中添加)。是否开 host 白名单。
* rpc-password: 字符串。RPC 密码。
* rpc-port: 数值（默认 = 9091)。RPC 端口号。
* rpc-url: 字符串（默认 = /transmission/. 在 2.2 版本中添加）。
* rpc-username: 字符串。用户名。
* rpc-whitelist: 字符串（逗号分隔的 IP 地址列表，允许使用 `'*'` 的通配符，例如：`“127.0.0.*，192.168.*.*”`，默认值：“127.0.0.1”）。
* rpc-whitelist-enabled: 布尔值（默认 = true）。是否启动白名单。

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
