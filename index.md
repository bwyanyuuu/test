---
tags: 108上
---
# CN + CCNA
[TOC]

https://sls.weco.net/CollectiveNote20/Network
## Introduction
### "Nuts and Bolts" View
● 億萬個 computing devices　　　　　　　　● communication links
　　◇ hosts = end systems　　　　　　　　　 　◇ fiber, copper, radio, satellite
　　◇ running network apps　 　 　　　　　　　◇ transmission rate : bandwidth
● packet switches 　　　　　　　 　　　　 　● Internet standards
　　◇ forward packets (chunks of data) 　　 　　 ◇ RFC : Request for comments
　　◇ routersand switches 　　 　 　 　 　 　　　◇ IETF : Internet Engineering Task Force
● Protocols 控制接收、發送訊息　 　 　　　　● Internet: “network of networks”
　　◇ Ex. TCP, IP, HTTP, Skype, 802.11 　　　　 　◇ Interconnected ISPs

### Network Structure
● network edge :　　　　　　　　　　 　 　　● network core:
　　◇ hosts : clients and servers　　　　　　　　 ◇ interconnected routers
　　◇ servers often in data centers　　　　　　　◇ network of networks
● access networks, physical media :　　　 　　 ● shared or dedicated (獨享)?
　　◇ wired, wireless communication links

    
    

### Access networks
- digital subscriber line (DSL) ![](https://i.imgur.com/JjYPygF.png =500x200)
    - < 2.5 Mbps upstream rate (通常 < 1 Mbps)
    - < 24 Mbps downstream rate (通常 < 10 Mbps)
- cable network
![](https://i.imgur.com/I1dtvnB.png =550x200)
    - frequency division multiplexing : 用頻率區分頻道
    - HFC : hybrid fiber coax
        - 30Mbps downstream, 2 Mbps upstream

- home network
![](https://i.imgur.com/yfgYLfn.png =460x300)

- Enterprise access networks
![](https://i.imgur.com/sUyO619.png =470x200)
    - 10 Mbps, 100Mbps, 1Gbps, 10Gbps
    - 通常連到 Ethernet switch

- Wireless access networks![](https://i.imgur.com/44TmeYh.png =550x270)

### Physical media
- physical link : 在送收端中間那條實體的線
1. guided media :
    - 訊號在介質裡傳播 : copper, fiber, coax
2. unguided media : 不需介質，例如：radio
- twisted pair (TP) (雙絞線)
    - 兩根絕緣 copper wires (銅線)
        - Category 5: 100 Mbps, 1 Gbps Ethernet
        - Category 6: 10Gbps
- coaxial cable (同軸纜線) :
    - 兩根同心銅導體、雙向
    - broadband :
        - multiple channels on cable、HFC
- fiber optic cable (光纖電纜) :
    - 玻璃纖維載有光脈衝 (light pulses), each pulse a bit
    - 高速運行 :
        - 高速點對點傳輸 (例如：10’s-100’s Gbps transmission rate)
    - 錯誤率低：
        - 中繼器相距很遠
        - 抗電磁噪聲
- radio link types:
    - terrestrial microwave (地面微波)：高達 45 Mbps channels
    - LAN (例如：WiFi)：54 Mbps
    - wide-area (例如：cellular)：4G cellular → ~ 10 Mbps
    - 衛星
        - Kbps to 45Mbps channel (或多個較小的通道)
        - 270毫秒的終端延遲 (end-end delay)
        - 地球同步與低海拔
### Network Core
- routing : 決定把封包送去哪
- forwarding : 把封包傳出去
#### Circuit Switching
- switch間很多條線，選一條拿到就獨享
- ![](https://i.imgur.com/JrnAD4G.png =400x230)
#### Packet Switching
- 可以容納更多人使用，因為不會每一刻都多人在用 → 提高效率
- 非常適合突發數據：資源共享，更簡單，無需建連線
- 可能出現過度擁塞：數據包延遲和丟失 → protocal 需要可靠的數據傳輸，塞車控制
#### 比較
![](https://i.imgur.com/OD0OO2N.png)
### 計算
![](https://i.imgur.com/htUObF3.png)
- $d_{nodal}= d_{proc}+ d_{queue}+ d_{trans}+ d_{prop} = d_{total}$ (sec)
- $d_{proc}$ nodal processing (< msec)：檢查 bit errors、決定要從哪個埠出去
- $d_{queue}$ queueing delay：
    - 排隊的時間，與交通壅塞度成正比
    - a：單位時間封包平均到達率 (pkt / sec)
    - $\frac{La}{R}$ ~ 0：延遲少
    - $\frac{La}{R}$ > 1：延遲多，封包到達速度比處理速度還快 → 永遠的延遲
- $d_{trans}$ transmission delay：
    - $d_{trans} = \frac {L}{R}$，**傳到 link 上所需的時間 (跟頻寬相關)**
    - L = 封包大小 (bits)
    - R = transmission rate (bits/sec → bps)
    - store and forward：這個封包的全部都到了才會開始往下一個地方傳
    - end-end delay = $\frac{2L}{R}$ (假設無 $d_{prop}$)
- $d_{prop}$ propagation delay：
    - $d_{prop}= \frac{d}{S}$，**在 link 上傳遞所需的時間 (跟線長相關)**
    - d = 這條線路的長度
    - S = 傳遞速度 (~2x108 m/sec)
- Band-width delay product = $R\times d_{prop}$ (bits) 
    - 在 link 中因為傳輸延遲可容納的 bits 數
- link 上能容納最大的 bit 數：band-width delay product 與 封包長度 的 最小值
- 在 link 每個 bit 的長度 $m = \frac {link長度}{最大bit數} = \frac{d}{R\times d_{prop}} = \frac{d}{R\times\frac{d}{S}} = \frac {S}{R}$ (m/bit) (並不會平均分散)
- 如果一個訊息分成 n 個封包(收到 ACK 才會傳下一分割)：$d_{total} = n(2d_{prop}+d_{trans})$
- Throughput：(bits / sec)，送收端之間的位元吞吐率，有瞬時與平均速率
    - ![](https://imgur.com/download/Xl72MKl)
    - R~s~ < R~c~ ![](https://i.imgur.com/fFwyQsT.png)
    - R~s~ > R~c~ ![](https://i.imgur.com/nAPiPFf.png)
    - end-end throughput = min(R~c~, R~s~, R/10) ![](https://i.imgur.com/d5hD1At.png)
### Layer + Protocal
|#|Layer|ISO OSI|Protocal|
|---|---|---|---|
|4|Application|7 Application<br>6 Presentation<br>5 Session|HTTP, FTP, SMTP...|
|3|Transport|4 Transport|TCP, UDP → 程序間的溝通|
|2|Network|3 Network|Internet protocal → IP → **Router** → host 間的溝通|
|1|Link|2 Data Link<br>1 Physical|Ethernet protocal → MAC address → **Switch**|
![](https://i.imgur.com/dyTefld.png)


## Application Layer
- 為何需要 port #
    - 因為 client 上會有很多 APP
    - 利用 port 來對應要送去給哪個 APP
### HTTP ( HyperText Transer Protocal )
#### use TCP
- client 初始化 TCP 和 server 的連線(建立socket)在 port 80
- server 接受 client 的 TCP 連線
- HTTP 訊息 (application-layer protocol messages) 在client 和 server 間交換
- TCP 連線關閉
- [註]：client → web browser... , server → web server...
#### Stateless : 
- 不會記住同一台腦上次所發出的request，每次都是重新的開始
- 紀錄狀態很難，且server重開會將狀態丟失
#### HTTP Connections : 
| Non-Persistent HTTP | Persistent HTTP |
| -------- | -------- |
| 1. client 發送建連線<br>2. server 收到並同意連線<br>3. client 發送 request<br>4. server 收到，然後發送response<br>　並關掉連線<br>5. client 處理發現回傳的物件<br>6. 再去建連線抓物件(重複1.~5.)|● 連線會在server發送**回應**後持續著<br>● client 就可以一直發送**要求**載物件<br>![](https://i.imgur.com/TV4FJ98.png)
|
|較耗時，因為每個物件都要算1次<br>response time = <br>2RTT + file transmission time<br>|較省時<br>較少RTT|
-  RTT ( Run Trip Time ) : packet 從 client 到 server 再到 client 去回所花時間
#### Request Message
![](https://i.imgur.com/tAPGVeV.png)
- General Format
![](https://i.imgur.com/gb2cOAD.png =440x250)
- Uploading form input (2種做法)
    - POST :
        - 網頁自身包括 form input
        - input 被上傳至 server 的 entity body
    - URL (用 GET) : 
    input 被上傳在 URL 的 request line 如下 
    `www.somesite.com/animalsearch?monkeys&banana`
- HTTP/0.9：GET，response request 之後立即關閉連接
- HTTP/1.0：GET, POST 
    - HEAD：要求服務器將 request 的物件置於 out of response
    - 增加 response 狀態碼, 標記可能的錯誤原因
    - 引入協議版本號、HEADER, 讓HTTP處理請求和響應更靈活
    - 傳輸的數據不再僅限於文本
    - 但並不是一個"標準",只是記錄已由實踐和模式的一份參考文檔,相當於一個"備忘錄".
- HTTP/1.1：GET, POST, HEAD
    - PUT：將實體主體中的文件上傳到URL字段中指定的路徑
    - DELETE：刪除URL字段中指定的文件
    - 增加了緩存管理和控制、明確了連接管理,允許持久連接
    - 允許 response 分塊(chunked), 利於傳輸大文件
    - 強制 Host header, 讓互聯網主機託管成為可能
- HTTP/2
    - 二進制協議, 不再是純文本
    - 可發起多個請求, 廢棄1.1中的管道
    - 使用專用算法壓縮頭部, 減少數據傳輸量
    - 增強安全性,事實上要求加密通信
    - 目前HTTP/2的普及率還比較低,主要是因為HTTP/1.1太經典和強勢
#### Response Message
![](https://i.imgur.com/0ImcsHr.png =550x300)
- status code : 
    - 200 OK
    - 301 Moved Permanently
    - 400 Bad Request
    - 404 Not Found
    - 505 HTTP Version Not Support

#### User-server State : **cookie**
- 每個人分一個unique ID，在資料庫紀錄這個ID所有的狀態
    (利用 cookie file 和傳遞的 cookie 來達成叫出狀態、使用、更新)
![](https://i.imgur.com/RZn9BPG.png)
- 4 要素 : 
    1. cookie header line of HTTP response message
    2. cookie header line in next HTTP request message
    3. 使用者端的 cookie file (由使用者的 browser 來管理)
    4. 背後連結的資料庫
- $Ex.$ 針對性行銷、可反查 source IP、購物車、授權

#### Web Caches (proxy server 代理伺服器) : 
- 在不要連到原伺服器的情況下滿足 client 的 request
- proxy 通常是網路提供者所架設
![](https://i.imgur.com/P2mSqJZ.png =300x200)
1. 第一次要求時，先到代理再到原伺服器走正常流程
2. 第二次如果有別人要求相同時(且代理的資訊還很新的時候)會直接從代理伺服器拿到資料就回去了
- 優點：
    - 減少 response time
    - 減少 link 上的塞車 (省頻寬 → 省錢)
    - 使 content provider (Ex. youtube, BBC) 能更有效率傳遞物件/資料
- Example 1 (no local web cache) : 
    - assumptions:
        - avg object size : 100K bits
        - avg request rate from browsers to origin servers : 15/sec
        - avg data rate to browsers : 1.5 Mbps (= 100K * 15 / sec)
        - RTT from institutional router to any origin server : 2 sec
        - access link rate (出LAN去外面的傳遞速率) : 1.54 Mbps
        - 1 Gbps LAN
    - consequences:
        - **LAN utilization** = 1.5Mbps / 1 Gbps = 0.15%
        - **access link utilization** = 1.5Mbps / 1.54Mbps = 99% **→ 問題所在**
        - **total delay** = Internet delay + access delay + LAN delay = 2 sec + mins + usecs **→ 太久**
- Example 2 (local web cache) : 
    - assumptions:
        - suppose cache hit rate is 0.4
            - 40% requests satisfied at cache
            - 60% requests satisfied at origin
        - 其餘條件與上面相同
    - consequences:
        - **data rate to browsers** = 0.6 * 1.5 Mbps = $0.9 Mbps$
        - **LAN utilization** = 1.5Mbps / 1 Gbps = 0.15%
        - **access link utilization** = $0.9Mbps$ / 1.54Mbps = $54\%$
        - **total delay** = 0.6 * (delay from origin servers) + 0.4 * (delay when satisfied at cache) = 0.6 * 2.01 + 0.4 (~msecs) = ~ $1.2 secs$
    - local host 維護成本較低，比增加 access link rate 還省錢，卻不失效果
#### Conditional GET
- 功能：如果 cache 是最新版就不要寄物件
- cache : 記錄此cache的出生時間`If-modified-since: <date>`
- server : 如果此時間符合物件最後改變的時間就回傳 `HTTP/1.0 304 Not Modified`
![](https://i.imgur.com/1zlW6be.png)
- 優點：減少延遲、頻寬占比

### Electronic Email
#### 3 major components:
- User Agents
    - mail reader 可撰寫、編輯、閱讀信件
    - $Ex.$ Outlook, Thunderbird, iPhone mail client
- Mail Servers
    - Mailbox : 存放幫使用者收到的信
    - Message Queue : 要寄出的信的佇列
    - **信都存在 server 裡**
    - client : sending mail server
    - server : receiving mail server
- Simple Mail Transfer Protocol (SMTP)
    - 使用 TCP 通常在 port 25
    - 只能發送和接收屬於7-bits ascii的資料
         → 要發其他檔案就先轉ascii傳出去，收的時候再轉回來
    - mail server的命名大多如左 → smtp.nctu.edu.tw:25
    - 比較：
        |HTTP|SMTP|
        |---|---|
        |pull|push|
        |ascii|ascii|
        |一個物件、一個訊息| 多個物件在multipart messages裡

#### 過程：
**1.** 用 user agent 寄信 by SMTP
**2.** 送到自己的 mail server 或是把自己當作伺服器
**3.** server SMTP 開啟 TCP 連線 with 對方的 mail server
**4.** 用 TCP 送到對方的 mail server
**5.** 對方 server 先幫忙收信 (分到該去的 mail box)，如果serevr剛好沒上線，就會一直幫忙重送
**6.** 等對方user上線後，他再用 POP3 / IMAP / HTTP  去她的 mail server 從他的 mail box 收信
![](https://i.imgur.com/I9S3pfy.png)

#### 實作 (不需要outlook...等等，打指令即可完成)
- telnet servername 25
- see 220 reply from server
- enter HELO, MAIL FROM, RCPT TO, DATA, QUIT commands
- $Example :$ 
![](https://i.imgur.com/OmeJgN3.png =400x250)
- 在 message body 裡，to 和 from 是可以隨便寫的，不用符合真正的來源和目的，header 上的才是真的
#### 接收會用到的3種protocal
- POP3 ( Post Office Protocol ver.3) [RFC 1939] 最普遍
    ![](https://i.imgur.com/D2Dfbi4.png =450x300)
    - 上述例子運用“download and delete” mode → 如果換client後無法重看
    - “download-and-keep” mode : 會把信件複製到不同的client
    - stateless across sessions
- IMAP ( Internet Mail Access Protocol ) [RFC 1730] 現在很少再用
    - 全部的訊息都存在 server
    - 允許使用者管理資料夾的信件
    - 利用資料夾名、使用者ID的對應來存使用者狀態
- HTTP：網路上的郵箱 Ex. Google、YaHoo!...

### DNS (Domain Name System)
#### 功能
- name & IP address 相互的轉換
- host aliasing 取綽號：host本身的名字但可能是同一個 domain 的機器，所以幫他取一個別名為 domain
- load Distribution : 例如google每次轉到的IP可能不一樣(有超過一台的server, 一台電腦可有多張網卡多個IP)，由DNS幫他做這件事情 **(如果收到別名，會去找別名的紀錄，再拿查到的真實名字，去找他真正的IP)**
#### Hierarchy 階層性
![](https://i.imgur.com/WM76kqC.png =550x180)
- 階層從後到前 www.cs.nctu.edu.tw → local → root → tw → edu → nctu → cs
- 而 root DNS 分布在世界各地共13個，由無法解決的 local DNS 來聯絡
- 從最近的 local DNS 開始問，他如果不知道就問 root
- root 再按照階層來指示他要去哪裡找
- www 只是個機器名字，上面跑網頁伺服器，也可以是 ftp、隨便取...等等
#### Name Severs
- top-level domain (TLD) servers
    $Ex.$ com, org, net, edu, aero, jobs, museums, country domains : uk, fr, ca, jp
- authoritative DNS servers (授權 DNS) → 普通的 DNS
    - 某組織自己的 DNS，用於對內部 IP 與 domain 的翻譯
    - 通常會由組織自己 or 服務提供者所設定
    - Ex. 系計中也有自己的 DNS
- Local DNS name server
    - 平常電腦 sent query 先去的DNS，通常會往近一點問
    - 不直接屬於 hierarchy、有存 cache
    - ISP 都有一個
        - Internet Service Provider $Ex.$ 住宅 ISP, 公司, 大學...等等
        - 又稱為 “default name server”
    - 作用像是詢問 hierarchy 的 proxy
#### 過程
- 2 種 query 的運作：
    ![](https://i.imgur.com/NTvMfpE.png =540x320)
- 可以用cache記住，減少重複問的時間，只是cache還是要有time out以保持資訊更新
-  TLD通常也會cache著，因為個數不多，變動性低
#### DNS Records & msg
- RR (resourse records) 包括 `(name, value, type, ttl)`
- type=A (最下層)→ `name = hostname, value = IP`
- type=NS (對於DNS的)→ `name = domain, value = 此 domain 之權威 DNS 的 hostname`
- type=CNAME (對於別名的)→ `name = alias name, value = canonical (real) name`
- type=MX (對於 mail server 的)→ `value = name of mailserver associated with name`
- Message format
    ![](https://i.imgur.com/VQEvmH3.png =430x250)
- Identification : 16 bit # for query, reply to query uses same #
- Flags :　● query or reply 　 　 　 　● recursion desired
    　 　 　 ● recursion available　　　● reply is authoritative
#### 建立新的 DNS 伺服器
- 在 DNS registrar $Ex.$ Network Solutions 註冊名字
    - 須提供 names, IP addresses of 授權 DNS
        - primary and secondary 通常都會用兩台，怕意外掛掉等等
    - 需放2個 RRs 在 **.com TLD** 裡
        - `(networkutopia.com, dns1.networkutopia.com, NS)`
        - `(dns1.networkutopia.com, 212.212.212.1, A)`
- create authoritative server type A record for www.networkuptopia.com
- type MX record for networkutopia.com
- **通常開公司必備3伺服器：Web, DNS, Mail servers**
    - domain name 很重要，此三伺服器，現今大多想得出來的都被註冊過了
    - Web：為公司向外的門面
    - DNS：管理公司內部的IP們
    - Mail Server：對外部聯絡時所用的正式公司專門郵件帳號們
    - 也可以把三種機器跑在同一台，用alias取三個名字即可
#### Attack DNS
- DDoS attacks
    - bombard root servers with traffic
        - not successful to date
        - traffic filtering
        - local DNS servers cache IPs of TLD servers, allowing root server bypass
    - bombard TLD servers
        - potentially more dangerous
- redirect attacks
    - man-in-middle：Intercept queries
- DNS poisoning
    - Send bogus relies to DNS server, which caches
- exploit DNS for DDoS
    - send queries with spoofed source address: target IP
    - requires amplification

### Video Streaming and Content Distribution Networks
#### Multimedia : video
- coding: use redundancy withinand betweenimages to decrease # bits used to encode image
    - spatial (within image)：記得顏色的值、他出現過的地方
    - temporal (from one image to next)：記得跟上一張比，不一樣的地方
- CBR (constant bit rate)：固定速度
- VBR (variable bit rate)：
    - 能壓就盡量壓，塞車時壓少、否則壓多
    - 但 bandwith 比較難處哩，忽大忽小
- Streaming stored video
    - MOD (Media On Demand) : 要看再看就好，不像平常有線電視播完就看不到了
    - Youtube : 收到資料收集到可以撐一下 (pre-bubble) 才會開始播放，然後邊播邊收 → 用TCP也行，有時間把塞車延後的洞補起來 (但比較適合非直播，delay的話不是那麼嚴重 - buffer starvation)
#### Streaming multimedia : DASH (Dynamic, Adaptive Streaming over HTTP)
- Server : 
    - 把檔案分成多個chunks(對應播放時間，例如十秒)
    - 然後用不同的方法儲存、encode於不同的rate
- Client : 
    - 一直偵測可用頻寬的大小
    - 如果網路頻寬變多了，就要求較高的畫質，否則相反
    - 如果快要buffer starvation時就趕快降低畫質...等
- 不需要交換器路由器的幫忙來完成這些事情 → End Host 的智慧
    - 儲存地點分布各地 → 找一個較近的 or 交通順暢的路線
#### Content Distribution Networks (CDNs)
- 可以加強使用者體驗 (需額外花錢)
1. 建立 mega-server
    - 把東西都存在這裡，要拿都來這裡拿
    - 連接他的網路線會特別擠
    - 如果他壞了就都不能用了(沒有意外的替代) singal point...
2. 建立 CDN
    - 在地理上相距有距離的地方都設一個server
    - 裡面存一些內容的copy
    - 然後叫client去離他比較近 or 路上交通不壅擠的倉庫裡拿檔案
    - 有可根據地域的文化來決定要儲存什麼風格的內容
    - 有名公司：Limelight
- OTT (Over The Top) challenges
    - from which CDN node to retrieve content?
    - viewer behavior in presence of congestion?
    - what content to place in which CDN node?
- 過程：![](https://i.imgur.com/FuErQzE.png)
- 舉例：Netflix
![](https://imgur.com/download/ji0qAaY)


### Socket Programming
- 為 application 和 end to end transport protocal 的溝通介面
- 主要兩種
    - UDP : 
        - 沒有連線概念、送東西前不需要先建連線
        - **datagram** : 是一塊一塊傳送的
        - ![](https://i.imgur.com/Tq9zm5s.png)
    - TCP : 
        - 每個連線建起來就會創造一個新的socket(用完舊的不會關掉)
        - 所以一個伺服器可以一次對多個client
        - 如果封包沒送好會幫忙重送
        - **in-order byte stream** (pipe) : 如果一塊一塊接收到，還是會把它看成一串byte(他看不出來是一塊一塊的)
        - 只判斷封包是否沒有少byte，順序對不對，有問題就會重送
        - ![](https://i.imgur.com/QVlhSAI.png)
    
### important themes:
- control vs. messages
    - in-band : 乖乖排隊
    - out-of-band : 加速處理(插隊) → 如果msg跟控制相關(就有時效性)
- centralized vs. decentralized
<br>
- stateless vs. stateful
<br>
- reliable vs. unreliable message transfer
<br>
- "complexity at network edge"
    - 把複雜的處理搬到 end host 上做
    - 讓 network core 越簡單越好 (所以如今就可以把路由器等越做越快)

## Transport Layer
### Transport Service
- 提供app process間邏輯上的連線(end to end transport) → 當作是有完整的把L3做好一定聯的到現實要考慮的事物
- network layer : logical communication between hosts
- transport layer : logical communication between processes
    - relies on, enhances, network layer services
- 不用在乎實體上的連線，與中間如何連線 → L3
### TCP
- 可靠的傳輸
- 如今TCP的control已經做到非常公平，不只能降，還可降到大家差不多多
    - 沒成功就一直重送，直到收到確認收晚整成功的訊息
    - in-order delivery (error control)
    <br>
    - congestion control
        - 交通壅塞時，queue裡東西太多賽不進去所以掉封包了
        - 解決：
            - 自私版：直接每次都多送，掉了還有替代的 (但很有效，會造成更壅塞)
            - 合作版：大家都降速，都送少一點，一直降到封包不掉為止，車少了交通自然較通順
    - flow control
        - 送東西時要考慮兩端的處理速度
        - 送太快的話，到收端時來不及處理就掉光光
        - 並非交通壅塞導致
        - 解決：收到要回覆是否有收到，知道收到在送下一個
    - connection-oriented：要達成三大目標必須先建連線(要先hand shaking)
    

### UDP (User Datagram Protocal) [RFC 768]
- 特性、用途：
    - 不可靠的傳輸，沒有三大 control (congestion / flow / error control)
    - best effort IP(底下的網路就是best effort), with no garantee
    - connectionless 不需要先建連線 (減少delay)
    - DNS、SMTP、streaming multimedia
    - 用於中間掉資料不會影響大局的事情
- segment header
    - ![](https://i.imgur.com/GT795Ls.png =300x200)
    - 單純 : 不需要記錄一些狀態來達成三大控制 → header 大小較小 
    - no congestion control : UDP可以根據需要快速消除
- checksum
    - 用來判斷錯誤
    - ![](https://i.imgur.com/cOXftUI.png)
    - check 之後不一定一定是無 error 的
    - $Ex.$ 兩個同時翻轉了就偵測不到，但同時翻轉的機率蠻低的
    - 把所有msg切成16bits一組全部加起來，overflow的要往後加
    - 最後的何在全部翻過就是checksum  `sum & checksum = 0`
    - checksum 位數越多，偵測的精準度越高
    - 但第二層也有 checksum (CRC 32 bits) 成功率 99.99% (其實多層把關)

- FM vs. AM
    - FM : 用訊號的頻率來判斷 0 or 1，較不被雜訊影響
    - AM : 用震幅來判斷 0 or 1，聽起來糊糊的
- TCP、UDP 都沒有的服務
    - delay guarantee、bandwidth guarantee
        - 但其實不是這層的範疇，是下層網路層的較物理的問題所致
    - 安全性，傳輸的訊息不加密
        - SSL：加密的 TCP，提供數據完整性、端點認證
### Multiplexing/demultiplexing
- Multiplexing：處理來自 multiple sockets 的訊息，加上 transport header (為了之後 demultiplexing)
- Demultiplexing：利用 header info 決定要分給哪個 socket
    - ![](https://i.imgur.com/VrLB0UB.png =200x200)
    - 接收時看port來決定要指派到哪個socket(socket對應bind某port)
    - UDP接收的時候只用一個socket
        - checks destination port # in segment
        - directs UDP segment to socket with that port # 
        - IP datagrams with same dest. port #, 但有不同 source IP 或 source port # 會被導向同一個 socket at dest
    - TCP接收時是一對一來源，多個來源，多個socket，且同一個APP可以在同來源目的下建立多個socket
        - 封包內容包括4個
            - src IP, port
            - dst IP, port
        - ![](https://i.imgur.com/JCeW3oD.png)
        - EX. FTP 會建一個來傳遞 FTP 的命令，當打完指令要下載檔案時，再開一個來專門傳送檔案的 socket
        - 如果不同的 socket 都綁在同個 port 上
        - 為了區分就辨識就四個內容一起看就可以完整分辨要分去哪個 socket
        - thread server : 用這個可以管理同個 port 上的多個 socket
- dst port & src port的填空


### Principles of reliable data transfer
- 所謂可靠的傳輸：資料不能掉、順序不能錯、位元不會翻
    - 因為底層無法做到，所以上層才需要去做
    - ![](https://i.imgur.com/eYQnCw6.png)
    - r / udt (reliable / unreliable data transfer)
- 先假設只有單向，需要傳 control packet ($Ex.$ ack packet)、data packet 
- 用 state machine 去決定他的狀態
- rdt1.0：有一個 reliable channel 的情況下
    - rdt_send()：等上層呼叫，就幫他傳出去
    - rdt_rcv()：等下層呼叫，就把 data 收進來
    - ![](https://i.imgur.com/gcVu4vb.png =450x100)
- rdt2.0：會有 bit errors
    - 可以把一群bits看成二維陣列，每行每列都做 parity bit，就可以直接看出哪個bits錯，收端看到自己改過來就好 (但TCP用 error detection，偵測到錯就重送)
    - acknowledgements (ACKs)：回復送端自己到無誤的封包
    - negative acknowledgements (NAKs)：告訴送端他傳的封包有誤 
    - 這兩種封包為 control packet，但如果她們也出錯，送端就看不出來她到底傳 ACK 還是 NAK
    - 所以悲觀一點，沒有收到 ACK 就重送 (但會有收端收到多份的問題 → 見 rdt2.1)
    - stop and wait：等到確定收到 ACK 才會繼續傳到下一個 (效能較差)
    - ![](https://i.imgur.com/ycURyqq.png =430x220)
- rdt2.1：封包送出時給編號
    - 用 sequence num 來判斷有沒有收到重複的 (只有 0 和 1，這樣夠用是因為它使用 stop and wait 而且一次一封包)
    - 0th → 0, 1st → 1, 2nd → 0 (10 overflow), 3nd → 1...etc
    - 但編號最好永遠不要繞回來，不然判斷可能會出錯
    - 兩倍的 state 量，因為要記得現在是 0 還是 1
    - 如果收端收到兩個一樣數字的封包就認定他為重複的就丟掉
    - ![](https://i.imgur.com/ppZRhje.png)
    - ![](https://i.imgur.com/YderZda.png)
- rdt2.2：單純化，只傳 ACK，不傳 NAK
    - 送回去的 ACK 裡要包括目前收到成功且最新的封包的 sequence num
    - 如果收到的號碼跟上一個 ACK 的號碼一樣就把最後傳送過的封包重送
    - ![](https://i.imgur.com/w1dEsWV.png)
- rdt3.0：有 error 和 loss
    - 送出去時開始計時，時間之內如果沒收到 ACK 就重送，重新計時
    - Timeout 的設定要很有學問，不能太短太長
    - ![](https://i.imgur.com/qxF57MO.png)
    - ![](https://i.imgur.com/IFI1gAt.png)
    - ![](https://i.imgur.com/qX7wtEf.png)
    - 1 Gbps link, $d_{prop}$ = 15 ms, 8000 bit packet:
        - $D_{trans} = \frac{L}{R} = \frac{8000 bits}{10^9 bits/sec} = 0.008 sec = 8 microsecs$
        - $U_{sender}$ (頻寬使用率) $=\frac{L / R}{RTT + L / R} = \frac{.008}{30.008}= 0.00027$
        - RTT = 30 ms, 1KB pkt every 30 ms : 33kB/sec thruput over 1 Gbps link
        - 頻寬大也無用，protocal 限制了實體
#### Pipelined Protocal：
- 一次送 n 個封包，$U_{sender}$ 會變成 n 倍
##### Go-back-N (GBN)：
- ![](https://i.imgur.com/t1yHNCj.png)
- n 的選擇：在RRT時間內可以在線上的最大封包數
- 送端：![](https://i.imgur.com/C5xH0ha.png)
    - 可以連續送 n 個 unacked 封包 (不等 ACK 的)
    - 要送第 n + 1 個封包時要等包括第 1 個封包的 ACK 回來 (nextseqnum 超過窗戶就不送)→ window-based
    - 開始送封包就開 timer，收到 cumulative ACK就把他 +1 當 send_base，把窗戶右移，然後關掉原本的計時器
    - 如果 timeout 就把全部的 unacked 封包 (從 send_base 到 nextseqnum - 1 的封包) 重傳，timer 重設
- 收端：![](https://i.imgur.com/tQhqtkP.png)
    - cumulative ack (TCP 使用)，送的 ACK seqnum 意思為她和她之前的都收到了
    - 收到未連續的封包們時(或其他奇怪的事情)，就回 ACK，包括的是此序列第一個缺少的 seqnum - 1，然後把封包直接丟掉
    - 是否照順序要比對 expectseqnum
- 缺點：只要中間有洞，後面全丟掉 (但接收端運作較簡單)
- Action![](https://i.imgur.com/nVMqWRx.png)

##### Selective Repeat:
- ![](https://i.imgur.com/QpEON0z.png)
- window size N，也是一次可以送 N 個 unacked 封包
- 送端：
    - nextseqnum 超過窗戶就不送
    - 每個封包有自己的 timer，如果 timeout(n) 就把 n^th^ 單獨重送，重開計時器
    - ACK(n) in [sendbase, sendbase + N] : 
        - 標示 n^th^ 封包已被收到，把計時器關掉
        - send_base == ACKseqnum：把窗戶右移，並把資料送給應用
- 收端：
    - ACK(n) 是個別的 (individual)
    - pktn in [rcvbase, rcvbase + N - 1]
        - 傳送 ACK(n)
        - out-of-order: 暫存在 buffer 裡
        - in-order: 把他到下一個洞之前的封包都給應用
    - pktn in [rcvbase-N, rcvbase-1]：傳送 ACK(n)
    - else：忽略
    - 收到窗戶之外的封包就拒收丟掉
- Action![](https://i.imgur.com/KYCda9K.png)
- 問題：![](https://i.imgur.com/v0Vbzxr.png)
    - 如果 ack 丟失，剛好接到對的 expectseqnum，就會收到兩份一樣的
    - 解決：seq_size > window_size 的兩倍，讓他沒機會重疊
### TCP
- 特徵：
    - point-to-point：一送端，一收端
    - reliable, in-order byte steam：沒有 “message boundaries” → 流
    - pipelined：TCP congestion and flow control **set window size**
    - full duplex data:
        - 雙向的資料流 (data flow) 於同一個連線裡
        - MSS：maximum segment size → $\tt 1500(MTU) - 40(Header) = 1460 bytes$
        - MTU：maximum transmit unit $\tt 1500 byte$
    - connection-oriented：在互相傳送資料前要 handshaking (交換 control msgs)
    - flow controlled：sender will not overwhelm receiver
- Header ![](https://i.imgur.com/5D2cm7F.png)
    - 可以同時扮演 DATA 和 ACK 和一些其他的空置封包角色！！！
- 傳送細節
    - sequence numbers：
        - 編號在 byte 上而不是在 pkt 上，以封包的 1st byte 的編號當作此封包的編號
        - 送的時候封包的大小可能不一樣 (不湊滿 1460 byte 也要送)
        - 共 32 bits，建完連線開頭選一個隨機值，不從 0 開始(經 queue delay 後可能誤收)
    - acknowledgements：
        - cumulative ACK (像 Go-Back-N)
        - 會把 out-of-order 的封包收起來 (像 selective repeat)
        - 收端回的 ACK 編號是最後一個 byte 的編號的下一號(收端回傳她期待收到的編號)
    - ![](https://i.imgur.com/60SEPcz.png =300x400)
    - Q：how receiver handles out-of-order segments
        A：TCP spec doesn’t say, up to implementor
    - 可以一次扮演兩個角色(收端和送端)，同一封包送 data 和 ACK
    - EX ![](https://i.imgur.com/Gyvh3pl.png)
- TCP round trip time, timeout
    - TCP timeout
        - longer than RTT,but RTT varies
        - too short：會多出一些不必要的重送
        - too long：對掉封包的反應太慢，浪費時間
    - $\tt SampleRTT$ 取得方法：
        - 送出去的時候開始計時，收到回來的時候停止
        - 把傳出去的時間放在封包裡，傳回來的時候在對應現在時間的 RTT(可以一次拿多個樣本，較佳) → 用 TCP 封包裡的 option 之 time stamp 來記錄
        - RTT包括 queue delay，會變動，測很多RTT來取平均
    - `EstimatedRTT = (1 - α) * EstimatedRTT + α * SampleRTT` 通常 $\tt \alpha = 0.125$
    - `DevRTT = (1 - β) * DevRTT + β * |SampleRTT - EstimatedRTT|` 通常 $\tt \beta = 0.25$ → safety margin 安全區間
    - `TimeoutInterval = EstimatedRTT + 4 * DevRTT`
    - 算出來的是 exponential weighted moving average
- 送端：![](https://i.imgur.com/htedJVg.png)
    - data rcvd from app： 
        - create segment with seq #
        - seq # 是 data 裡的 第一 byte 在原資料裡是第？個 byte
        - 如果沒再計時的話就 start timer
            - think of timer as for oldest unacked segment
            - expiration interval: TimeOutInterval
    - timeout：重送那個導致 timeout 的封包(最左邊沒 ACK 過的那一個封包)，重新計時
    - ack rcvd：更新 ACKed 的編號，如果還有 unacked 的片段就再計時
- EX： ![](https://i.imgur.com/3zgWGrh.png)
- 其他處理![](https://i.imgur.com/YPV0n7Q.png)
    - 如果目前沒缺 → delayed ACK (等一下看有沒有下個封包再送)
    - 收到正常順序的封包 → 每收兩個封包再回一個 ACK
    - 收到順序不對的封包 → 馬上發送 duplicate ACK (ACK 編號跟上次一樣的封包)
    - 收到把缺的補齊的封包 → 馬上發正確的 ACK
#### TCP fast retransmit
- 利用 cumulative ACK 的特性，有缺口時 ACK 的編號會重複送
- 如果收到三個一樣的ACK編號，就直接重送，不要等超時 → 快很多
- 適合連續送的資料(太少資料及不到三個也沒用)
- 三個的選擇
    - 太小：順序錯但都沒掉
    - 太大：跟等超時差不多
- ![](https://i.imgur.com/ZL1ZOvN.png =280x400)
#### Flow Control
- 每個 socket 有兩個 buffers
    - send buffer：拿來儲存要送出去的封包 
    - recieve buffer：收到封包後先存在這裡，應用要用的時候再呼叫 system code 來 buffer 裡取
- 可見收的時候是有限空間，太多擠不進 buffer 的時候就被丟掉了
- $\tt RcvBuffer$ size set via socket options (預設 4096 bytes)
- $\tt rwnd$ value：buffer 中剩下的可用空間，放在 ACK 裡送回送端 (recieve window)
- **送端藉由把 window size 改成跟 $\tt rwnd$ 一樣來達成**
- 所以其實 window size 跟 RTT & rwnd 都有關

#### Connection Management
- 2-way handshake 失敗例子： ![](https://i.imgur.com/s9Ixc8A.png)
    - 形成單方面的建連線、造成不必要的重送和重複收
- TCP 3-way handshake (FSM) ![](https://i.imgur.com/IVrcDmx.png)
    - SYNbit 和 ACKbit 設為 1 來帶有對於 SYN 的 ACK 的作用
    - SYN flood 攻擊：送端故意送一個而不送兩個(不完成第三步握手)，讓伺服器挖出一個空間讓你等不到，然後送很多份讓你爆掉，癱瘓你原本該做的事情
    - 流程：![](https://i.imgur.com/5jOY5Ug.png)
- 關連線 → 需 4-way
    - 關可以單邊關，兩邊都關才是全關
    - 運用 FINbit 來達成
    - 過程 ![](https://i.imgur.com/rPn0Qwf.png)
    - 為何要在 TIMED_WAIT 再等一段時間？
        - 如果過去的 ACK 掉了，對面會再發一次，這樣才有機會再重送
        - 如果不等而太快關掉，然後又太快建起來，就有可能誤收，所以在等的時候霸佔那個 port 就不會發生這樣的事情
    - 為何是兩倍？
        - 因為兩倍已經很多了，關於 IP 層的 TTL
#### Congestion Control
- (1)：![](https://i.imgur.com/YEBhij2.png)
- (2)：
    - 1 router, finite buffers
    - $\lambda _{in} = \lambda _{out}$ for application-layer
    - transport-layer input includes retransmissions ${\lambda _{in}}' \ge \lambda _{in}$
    - 理想狀態：
        - perfect knowledge：只在 buffer 有空時才送封包
        - known loss：buffer 滿了就會把再來的封包丟掉 → sender 只重送被丟掉的封包
    - 現實上duplicates
        - packets can be lost, dropped at router due to full buffers
        - 太早超時，造成發送兩份都被收到，浪費頻寬
    - 代價 $\tt goodput$ (每單位時間接收到的"有用"資料)：![](https://i.imgur.com/Bz9EE83.png)
        - $\tt unneeded$ $\tt retransmission$ (重送一些不須重送的)
- (3)：![](https://i.imgur.com/jb9IfDI.png)
    - 4 senders、multihop paths、timeout/retransmit
    - 中間經過別的地方時，某些路段可能有其他人在競爭
    - 另一代價：浪費前面的頻寬，然後在後面的 router 太擠被丟掉，不如來送其他的封包
    - $Q$：當 $\lambda _{in}$ 和 $\lambda _{in}$’ 增加時會發生甚麼？
    - $A$：當紅的 $\lambda _{in}$’ 增加時，所有藍色要到達的封包都被丟了(因為被占滿了)，blue throughput → 0
- 由此可知，壅塞是很嚴重的問題，付出許多代價
    - 重送的浪費頻寬
    - 被丟掉時，此封包曾經過的上游的頻寬就功虧一簣浪費了
    - 所以應該要共體時艱，一起降速，不要 retransmission
- AIMD 方法 (additive increase multiplicative decrease)：
    送端增加傳輸速率 (window size) 來偵測可用頻寬，直到丟失發生
    - additive increase：一包一包的增加傳輸速率 ($\tt cwnd$) 直到封包掉了就砍半，如果都沒掉就認為他還有頻寬可以送
    - multiplicative decrease：封包掉了後就 $\tt cwnd$ 砍半(為了緊急舒緩網路塞車)
    - 這方法是 fast trasmission 有發揮作用的狀況下有用
    - TCP 天生就是設計來被掉封包的 ![](https://i.imgur.com/gb5sTCc.png =430x200)
- TCP Slow Start (其實是快速開始)
    - 一開始 cwnd = 1 MSS
    - 之後每個 ACK 回來就把 cwnd * 2，指數成長，直到第一次丟封包
- TCP 自身實作
    - sender limits transmission：$\tt LastByteSent-LastByteAcked<cwnd$
    - 粗估 TCP 傳送速率 $\tt rate=\frac{cwnd}{RTT}$ bytes/sec
    - timeout 表示的丟失:
        - 一開始 cwnd = 1 MSS
        - 先用 slow start，直到**門檻值 (threshold)** 再用 linearly (AIMD)
    - 3 個重複的 ACKs 表示的丟失：TCP RENO
        - dup ACKs 表示網路可以傳送東西
        - cwnd 切一半然後用線性成長
    - TCP Tahoe 則是掉包設 cwnd = 1 (兩種情況都如此)
    - switching from slow start to CA (**C**ongestion **A**voidence)   ![](https://i.imgur.com/94bZKYo.png =430x260)
        - 掉封包時，$\tt ssthresh$ (緩啟動門檻值) 設為 1/2 * $\tt cwnd$，且 cwnd 再從 1 開始
        - 在門檻值之前用 slow start，超過後用 AIMD
    - state diagram![](https://i.imgur.com/SPI9Cyx.png)
    - TCP 只要封包掉了就假設他塞車，如果沒有就加速充分利用
        - 但丟封包不一定是塞車，如果在無線網路有可能是訊號差...等問題
- TCP throughput
    - 忽略 slow start，假設一直有資料可送
    - W = 丟失時的 window size (bytes)，跟底下可用頻寬有關(正相關) (人多的時候就較小)
        - avg. window size (# in-flight bytes) is ¾ W
        - avg. thruput is 3/4W per RTT
    - $\tt avg\ TCP\ thruput = \frac{3}{4} \frac{W}{RTT}\ bytes/sec$
    - 最理想狀況，都是觸發 fast trasmission，而不是 timeout ![](https://i.imgur.com/hiAdTML.png)
- TCP Futures：TCP over "long, fat pipes" (長距離，大頻寬)
    - Ex：1500 byte segments、100ms RTT、 10 Gbps throughput
    - 需要 W = 83,333 in-flight segments
    - throughput in terms of segment loss probability, L [Mathis 1997]:
        - $\tt TCP\ throughput =\frac{1.22\times MSS}{RTT\sqrt L}$
        - 為達成 10 Gbps throughput，需要 loss rate of L = 2 * 10^-10^ (很小的遺失率)
    - new versions of TCP for high-speed
- TCP Fairness
    - 最理想狀態是平均分配給每個 sessions
    - 大部分的情況下，頻寬的分配會是均勻的 (不能看瞬時，會不準)
    - 但還是有可能發生霸凌狀況 → 當兩邊的 RTT 不同的時候，RTT 大的比較佔優勢
        - 前言：觸發 fast transmit 時會比觸發 timeout 還要快，可以少等一些時間，如果一邊一直觸發，另一邊一直沒觸發，沒觸發的那一邊就被霸凌了！
        - 當 RTT 較大的時候，window size 可以比較大，掉封包的時候後面有很多封包可以幫她集到 3 個
        - 當 RTT 較小的時候，能同時在線上傳輸的封包較少，可能無法集到三個而導致她就需要一直等超時 → 就被霸凌了！
    - 不同協定本身的傳遞特徵差異導致的不公平
        - UDP 的話可以定速
        - TCP 相比起來比較吃虧，因為會一直降速
- Explicit Congestion Notification (ECN)
    - IP header 用 2 bit 來顯示中間 router 的狀態，然後一路傳下去到收端，收端回 ACK 傳到送端(裡面包含 ECE 顯示收到封包裡所傳達的交通狀態)，讓送端知道路上有遇到塞車
    - 送端收到塞車封包後 → 同掉封包的處理方式來進行(但封包其實沒真的掉)
    - 基本上作業系統與近年來的較先進的路由器等等都有此功能，不過只有 IOS 有預設開啟
## Network Layer
### Overview of Network layer
- network-layer functions
    - routing：決定把封包送去哪個輸出端 (演算法-找router的shortest path)
    - forwarding：把封包從輸入端送到輸出端
- Data plane
    - local、per-router function
    - 決定如何將來到輸入端的 datagram 送到輸出端 → forwarding function
- Control plane
    - network-wide logic
    - 決定如何在路由器之間將 datagram 從 src host 到 dst host 的 end-end path 路由
    - **Per-router control plane** (traditional routing algorithms)：
        - 實作於路由器，會看到**離散**的電腦或路由器...等等
        - 每個路由器都有 routing table，各自交換訊息以得到其他路由器的資料再合併得到最佳的路徑，不需匯集所有資料再一台電腦上就可以進行
        ![](https://i.imgur.com/mHGsGmK.png)
        - 目前大多數的網路運用此方法
    - **Logically centralized control plane** (software-defined networking (SDN))：
        - 實作於 (remote) servers，回歸到單一電腦決定整個網路的運作，只讓一台有智慧，其他人都是白癡，全部都聽他號令
        ![](https://i.imgur.com/eE2fP7S.png)
        - 邏輯上只有一台 (primary)，但物理上會有備案的那一台 (secondary)，當今天這台壞掉，還有人可以接替他的工作
        - 缺點：一台電腦可負荷的路由器通常 200 多台就是極限了 → 無法構造大型網路
        - 目前主要運用在 data center 的網路(封閉、同質性高)
- Network service model
    - in-order datagram delivery
    - guaranteed minimum bandwidth to flow
    - restrictions on changes in inter-packet spacing
    - 在同一個 flow of datagrams 上可能因為中間的延遲...等等，封包間的間隔時間會變動 (jitter 抖動) → 網路如果使間隔時間改變是不行的，尤其對於影片和音樂等等，會跟著延遲
    - 甚麼都沒有保證 → best effort ![](https://i.imgur.com/43Ao3fd.png)
    - ATM (Asynchronous transport mode)：他想提供一個有保證的網路，想取代原電信網路的 circuit switching → 並不通行
        - UBR (Unspecified Bit Rate)：對傳輸速率沒有指定，但可靠性要求很高，即 Best Effort，用於局域網仿真(LAN Emulation)
        - CBR (Constant Bit Rate)：有固定的帶寬(速率)要求，適用實時的話音和視頻信號傳輸
        - ABR (Available Bit Rate)：只需指定峰值(Peak)和谷值(Minimum)信元速率，應用不多
        - VBR (Variable Bit Rate)：允許隨時可變的帶寬，但必須指定峰值帶寬、最大突發數據長度和必須維持的最低速率(為了影片)

### Router 內部
![](https://i.imgur.com/yJIGQBY.png)
- **Switch Fabric Capacity**：bits per second ($\tt bps$)
    - 因為通常是 full duplex (雙向可同時進行)，所以通常實際上是他的 2 倍
    - 線上能同時通過的最大資料量
- **Forwarding Rate**：packets per second ($\tt pps$)
    - 在隨機封包大小下，他能做到的查表速度
- 在理想的情況下，是線的傳輸上限限制了速度(假設查表查很快的情況下)
    - 但因為幾乎沒有廠商可以把路由器的查表做這麼快 → 路由器以 pps 記規格
    - 故通常是查表速度影響整體速度 (查表所需的高速記憶體是非常貴的)
- 每個埠都有輸入和輸出的功能
    - 十年前這些操作是做再輸入端 → input buffer
    - 現今的都放在輸出端 → output buffer
    - 每一代的技術都對應不同要求，視要求來選購
- Input port functions ![](https://i.imgur.com/8KwBOP4.png)
    - 每個埠都有自己的表，好處是可以平行處理 (用空間很貴很快，換時間)
    - destination-based forwarding：僅基於 dst IP 來 forward (traditional) ![](https://i.imgur.com/C5tXJ5F.png)
        - 把同一個網段/區間當一個 entry 就可以省 2^16^ (/16) 的空間 (不用每個IP都特別記) ![](https://i.imgur.com/1C3ZZVl.png)
        - Longest prefix matching (LPM)：最長配對，如果有多個都配對到，就送給 net mask 較大的 → 更明確的路由
        >longest prefix matching: often performed using ternary content addressable memories (TCAMs)
        >content addressable: present address to TCAM: retrieve address in one clock cycle, regardless of table size
        >Cisco Catalyst: can up ~1M routing table entries in TCAM
    - generalized forwarding：用 header field values 來 forward
        - 每個 router 都有個 flow table 由一個大腦電腦來計算與給定
- gateway 會定在路由器上或 L3 switch
- 有較多特殊功能：VPN、NAT
- Routing table：Dst IP、mask、gateway、Interface (介面，要出去的出口)、meric (測量值，表示路徑遠近)
- 自我學習 : 
    - 但是是藉由 spanning tree 演算法 (STP) 來算出節點間的距離
    - 就是特地發封包，來更新 forwarding table
#### Switching fabrics (交換的方法)
- switching rate：pkts 從輸入端 → 輸出端的傳遞速率
    - 通常以輸入/輸出的 line rate 的倍數來衡量
    - N inputs：switching rate N times line rate desirable
- 三種類型：![](https://i.imgur.com/reShRqt.png)
- Memory：![](https://i.imgur.com/LpF9AV0.png)
    - 用普通電腦的linux，轉 switch mode 就可以用了
    - 把封包存在記憶體裡，然後用應用程式讀他，來決定要分給哪個介面，再從那裡送出去
    - 需要寫一次、讀一次
    - 會被記憶體侷限，適合每個埠頻寬小、總埠數少
- Bus：
    - 不要寫進記憶體哩，直接就從輸入介面到輸出介面 (by shared bus)
    - 同一時間一條 bus 只能容納一個 pkt
    - 被 bus bandwidth 侷限
- Crossbar：
    - 用多條 bus 平行使用，克服 bus bandwidth 的限制
    - 會切成多個固定長度的 cell 來傳送，到輸出端再合起來
    - 同時間有很多條路可以走，比較不會塞車
    - 但到同一個輸出端一定會經過同一段 bus

    
#### Queuing
- Input port queuing ![](https://i.imgur.com/qioWsm8.png)
    - 在輸入端排隊，送到對的輸出端就送出去，但有 HOL 問題
    - Head-of-the-Line (HOL) blocking：沒辦法同時傳送兩個不同輸入的封包到相同輸出
        Ex. 下面的紅色就要等上面的紅色傳完才能繼續傳
        　 → 但如果一開始就送綠的，整體效率會比較好
    - 輸入端的 buffer 是 FIFO(最便宜)
    - 效率低，所以現在很少人用輸入端來做交換
- Output port queuing ![](https://i.imgur.com/pKCNL2z.png)
    - 先從輸入分到輸出，再在輸出端才排隊，buffer 放在輸出端 → 沒有浪費時間等待的問題
    - 如果 buffer 沒有空位就會 drop，buffer 是用來接納突然的暴衝
    - 如果 buffer 弄得很大的確可以容納較多封包，但 queuing delay 會變很大 (如果再加到更大就跟電腦沒甚麼差別了，不需要)
    - ![](https://i.imgur.com/IYB2XkE.png)
    - buffering：當 datagrams 從 fabric 的速度大於傳出去的速度 (transmission rate) 就需要
        - Datagram (packets) 會因為 congestion 而弄丟 → 稀少的 buffers
    - scheduling：有規則的選擇要傳哪個 queue 裡的 datagram
        - 達網路中立性 (network neutrality)
    - RFC 3439 rule of thumb: average buffering equal to “typical”RTT (say 250 msec) times link capacity C
•e.g., C = 10 Gpbs link: 2.5 Gbit buffer
recent recommendation: with Nflows, buffering equal to $\tt \frac{RTT\times C}{\sqrt(N)}$

- scheduling：choose next packet to send on link
    - FIFO (first in first out) scheduling：一到達的順序送出，目前都是用這個，進不來的丟掉，便宜
    - discard policy：封包到達一個滿的 queue，要怎麼決定要丟掉誰？
        - tail drop：丟掉最後來的
        - priority：依據 priority 高低來判斷
        - random：隨機丟
    - priority scheduling：選擇優先度高的封包先送出 ![](https://i.imgur.com/ALTl78B.png)
![](https://i.imgur.com/7SgL04y.png)
        - 多種 class，每一種有不同的 priority，一個 class 一個 queue
        - 封包到了先以標頭裡的 class 記號分類
        - 高優先的封包還有就不會處理低優先的
        - 第二通行，沒其他那麼貴但又有功能
        - 題外話：`CPU schedualing 解決 starving → 如果在低優先度的佇列裡等太久都送不出去，就把它改成高優先，防止他永遠送不出去`
    - Round Robin (RR) scheduling： ![](https://i.imgur.com/qYkkcGA.png)
        - 多種 class，每一種有不同的 priority，一個 class 一個 queue
        - 有幾個 queue 就輪流每個 queue 取一個封包送
        - 較公平
    - Weighted Fair Queuing (WFQ)：有權重的 Round Robin ![](https://i.imgur.com/c5wAGvj.png)
        - 每個 queue 分配不同大小的頻寬比重，依比重來分配
        - 要考慮封包數和封包內容大小
### IP
- 總覽 ![](https://i.imgur.com/j9t5wqR.png)
- 封包格式 ![](https://i.imgur.com/5EOsxIH.png)
    - **Vers (version) :** (4 bits) iPv?
    - **HLEN :** (4 bits) header 總長 (in unit of 4 bytes)
    - **TOS (Type Of Service) :** 
    - **Total Length :** 16-bit, header + data of IP datagram. (? bytes)
        - limits the datagram to at most 65535 bytes
    - **Flags :** (3 bits)
        - bit 0 : 保留未定義
        - bit 1 : Don't Fragment (DF) ? 1 : 0
        - bit 2 : More Fragment (MF) ? 1 : 0
    - **Fragment offset :** (13 bits) 在原封包中的位移量，以byte為單位
    - **Time to Live (TTL) :** (8 bits) 預設 64 hops，遇到一個路由器就減一
    - **Upper layer**：寫接下來跟的是 TCP、UDP、ICMP…等等的 header
    - **Header Checksum :** (16 bits) error (corruption) detection method
    - 每個 router 上都有一個 forwarding table，到每一站都要找路，source host 無法決定走哪條路到達目的地，由網路層自行決定怎麼走。 (如果中間有掛掉，會自己換條路走，較優)
    - 除非使用 option 中的 source routing (分兩種)，source host可以決定， 循著已寫好的路走，可以 1.寫死 2.指定必經的某幾點，其他隨意。 (缺點是寫好的 router 掛掉，路會不通)
- IP fragmentation, reassembly ![](https://i.imgur.com/OvZoiRe.png)
![](https://i.imgur.com/6LlHiX0.png)
    - 藍色是 header、紅色是 data
    - link 上 MTU(max. transfer size) 的大小設定
        - 太大：整個頻寬都被占
        - 太小：header overhead，標頭占整個封包比太大，浪費頻寬
    - 從大 MTU 走到小 MTU 的 link：就要把封包切塊
        - 每個分割包可能會走不同的路，都到達目的地才會再組合起來
        - 切完之後在 IP 標頭裡 fragment offset 裡改成它的分割的編號
        - 從 0 開始數，第二包編號為第一個 byte 在原封包的第幾 byte 在除以 8 (只算資料部分，不算標頭)
        - 也會在裡面表示**此分割包後面是否還有分割包** → `fragflag == 1 ? 有 : 無`
    - 封包分割範例分析 ![](https://i.imgur.com/5OTwH9t.png)

        - 原本 4000 → data 3980，扣掉 header 20 bytes
        - 1500 → data 1480、offset = 0、fragflag = 1
        - 1500 → data 1480、offset = 1480 / 8 = 185、fragflag = 1
        - data 剩 3980 - 1480 * 2 = 1020 → + 20 = 1040 總長、 offset = 2960 / 8 = 370、fragflag = 0
#### IP addressing: introduction
- interface (介面)：用來連接 host/router/physical link，L3 的介面才會有 IP(或是 HOST)
    - router 通常有多個 interfaces
    - host 通常有 1 個 或 2 個 interfaces (例如：有限的 Ethernet、無限網路 802.11)
    - ![](https://i.imgur.com/ibtpiOg.png)
    - switch的port沒有 IP adress， blue tooth 也沒有
- Subnets：
    ![](https://i.imgur.com/GSdXfmc.png)

- 32-bit IP address
    - classful 看前幾個 bit 就可以知道他是哪個 class
        - class A：/8
        - class B：/16
        - class C：/24
    ![](https://i.imgur.com/91anu0w.png)

    - CIDR (Classless InterDomain Routing)：
        - /XX 可以不是 8 的倍數，可依需求切網段
        - adress format : a.b.c.d/x
        - ![](https://i.imgur.com/t1vvb4K.png)

- broadcast：在自己的 LAN 廣播、傳到遠端的 LAN 廣播
- 網路遮罩 netmask : 
    - IP AND mask 得到網路位址 → **網路位址相同才算在同一個LAN**
    - 192.168.2.3/24 → 24 叫 prefix
    - 192.168.2.3/11111111.11111111.11111111.00000000 → 遮罩有 24 個 1 所以寫 24
    - 192.168.2 裡共有253個IP
- 子網路分割 subnetting : 
    - ClassC：平時前 24bit 是網路位址, 後 8bit 是主機位址 -> 遮罩(mask) 255.255.255.0
    - 調整幾個 bit 的 networkID 來調整控制一網段下幾台電腦，用 /num 來表示拿幾 bit 來當 nwid
    - 192.168.2.3/27 -> (24+3) bit -> 8 subnet, 32 Host
    ![](https://i.imgur.com/KxF1nc0.jpg)
    - 對 subnet 總 IP 數要扣掉 **網路位址(第一個 IP)** 和 **廣播位址(最後一個 IP)**，共2個
    - 對可用 HostIP 要扣掉一個選出來的 Default Gatewy Address
- supernetting : 把網路合併，使 prefix 變小即可
- gateway
    - 發現目的地 IP 不在自己所在的 LAN 裡面時(用遮罩 and 看看)，就送到 gateway
    - if ip 遮罩(EX. 設/24但應是/25)亂設，別的LAN裡的電腦傳給你然後要回覆的時候，會因為自己以為對方在自己 LAN 裡就直接 ARP，想要直接用 mac 對傳，而不是送去他所在的 LAN 所以送不回去
    - if /25 第一個IP會是128，通常第一個和最後一個IP不會用，然後gateway會是第一個可以用的或最後可用的 → .129 / .254
### Dynamic Host Configuration Protocol (DHCP)
- Before DHCP (DHCP → extension of BOOTP)
    - 手動分配
    - Reverse ARP (RARP) → 過時，將 IP 分給 MAC
    - BOOTstrap Protocol (BOOTP) → 通常是靜態的，較少與IP相關的配置
- 動態分配IP，也有提供靜態的。任何連到這個網路的裝置就能得到網路相關資訊，適用 UDP 的實作
    - 有時效性 
    - 同一個IP adress過期後，如果沒有reuse，會給別人用 
    - 缺點:兩個users用同一個IP adress?? ack送得出去，卻收不到回復(可能回錯) 
- 可以用 relay agent 來服務其他 LAN 的電腦，就不用每個 LAN 都架一個 DHCP server
 ![](https://i.imgur.com/7jUNSHQ.png)
    - 要動態取得的功能，此網路上必定要有DHCP server
- 過程：
    - host → broadcasts **DHCP discover** msg [optional] (UDP port 68)
    - DHCP server → responds with **DHCP offer** msg [optional] (UDP port 67)
    - host → requests IP address：**DHCP request** msg (UDP port 68)
    - DHCP server → sends address：**DHCP ack** msg (UDP port 67)
     
     ![](https://i.imgur.com/7GMpCEL.png)
        
- 細節：
    - 外面包的是 UDP，廣播的時候是用 L2 的 FF:FF:FF:FF:FF:FF (MAC)
    - DHCP 回傳時可不只 allocated IP，還可包括 gateway IP、DNS sever IP、network mask
    - DHCP request 依序封裝 (encapsulated) 在 UDP → IP → 802.1 Ethernet 裡 ![](https://i.imgur.com/Rux7DOH.png)
- 範例 ![](https://i.imgur.com/RgV6U70.png)
- IP adresses : how to get one? ![](https://i.imgur.com/nbeIqNZ.png)

- Hierarchical addressing 
![](https://i.imgur.com/oeMxmzF.png)

    - Route Aggregation 聚合：if 在自己階層下的目的地(網段)，會把所有網段合併(if has auto summention)，跟外面講都送來我這 → 收縮到同一團
    - 奇怪的特例：![](https://i.imgur.com/i6P8ou6.png)

        - 要把特例告訴別人，但會使 routing table 裡面變較多
        - ∵ 路由用 longest prefix matching (LPM) 就能把封包送到那個特例
- 好處：不需人力，自動完成，好管理 (網管看紀錄就甚麼都知道了)，支援攜帶性裝置
- ![](https://i.imgur.com/0K5lTCl.png)
- Lease Renewal Times ![](https://i.imgur.com/7OVUMKT.png)
    - T1 < T2 < Lease time
        - T1 default value = 1/2 of lease time
        - T2 default value = 7/8 of lease time
    - Communicated via DHCPOFFER, DHCPACK
        - Client actions when times elapse
        - T1: client must renew address with the DHCP server
        - T2: client must renew address with any DHCP server
        - Lease time：client must stop using IP address
- DHCP Relay
    - ![](https://i.imgur.com/2YnH0Jb.png)
    - 中間的路由器要 config 讓 DHCP 的廣播可以過去另一邊
    1) DHCP client 在 local link 上廣播
    2) DHCP Relay Agent 收到然後 unicasts 他收到的訊息給 DHCP servers
        - Stores (fakes) 他自己的 IP address 在 DHCP 封包裡的 GIADDR 
    3) DHCP server 利用 GIADDR-value
        - 辨認送出來的封包是在哪個子網段，再依子網段分配 IP
        - 用 unicast 回覆給 GIADDR-address
    4) DHCP Relay Agent 再把回應回給原本發送的裝置
    5) DHCP Client 收到被分配的 IP，不知道中間有一個 Relay
### Network Address Translation (NAT)
- 把 prtivate IP 轉成外部的 IP，用註冊過的 IP 放外面來跟外部溝通(裡面的外面是連不到) ![](https://i.imgur.com/Zw2ELvV.png)

    - 內部網路不需要知道 NAT，外面也不用知道裡面就可以運作，內部自己獨立，還有安全，外面怎麼換都沒關係，這樣就可以減少 IP 的消耗
    - 註：IPv6 本來是為解決 IP 不夠用的問題，用 128 bits
- NAT router 上實作：![](https://i.imgur.com/13veEZv.png)

    - NAT translation table：記住每個 src IP、port # 對應的 NAT IP、new port #
    - 出去的 datagrams：src IP、port # → NAT IP、new port #，對方會以收到的 IP 來回覆
    - 進來的 datagrams：dst NAT IP、new port # → src IP、port #
    - 可能對外只有一 IP，那轉進來就看 NAT 怎麼分配，裡面哪台壞了都跟外面沒關係
    - 把自己切成 inside (loacl IP) 和 outside (global IP) 兩部分
    - 可以 statical config，也可以 dynamical 有連線再分配給你，還有防火牆的功能
- NAT overload
    - 用 Network Address Port Translation (NAPT) 或 Port Address Translation (PAT) 來完成 ![](https://i.imgur.com/jkQorjB.png)
    - 把多個沒註冊的 IP，對應到一個有註冊的 IP (多對一)
    - NAPT：包含 IP、protocal、port
    - fi-tuple：兩IP、兩port、一protcal，這樣就可以獨一無二的建造一個資料流(flow)
- Dynamic NAT 和 NAT Overload 都是動態對應
    - Dynamic NAT 是 one-to-one，NAT Overload 是 many-to-one.
- port reserving：不改變你的 port，那別的 IP 的對應這個 port 的對應表就會把它對應到別的埠上去
- Source NAT (SNAT)：在決定 routing **之後**執行
    - 改變 Src IP，dst IP 不變 → 讓裡面連去外面
- Destination NAT (DNAT)：在決定 routing **之前**執行
    - 改變 dst IP，src IP 不變 → 讓外面連到裡面
    - port forwarding：把裡面對外面的 IP 的不同 port 對應到內部不同的 IP
### Routing Protocol & Static Route
- routing algorithm + forwarding table
    - 用演算法算出把下一步 (out port) 放在表裡
- Destination Based Route ←→ Policy based 另外寫規則，可依 IP 以外的東西
    - Next-hop Routing：只存 **addr of next hop**，而不是完整的路由
    - Network-Specific Routing：存 **netid** 而不是 **hostid** (減少 entry 數)
    - Host-Specific Routing :
        - 儲存 **destinㄚation host address**
        - 可以有較多的控制(為了安全等等)
        - 雖然效率降低，但有更多優點
    - Default Routing：都找不到時就往那邊丟
- Inter & Interdomain routing ![](https://i.imgur.com/bOPHSVr.png)
    - Autonomous system (AS)：
        - 網際網路分成多個 AS，連線到國際的話，AS 要是唯一的，要申請
    - Intra-domain (AS) routing：AS 裡的路由 → Interior Gateway Protocol (IGP)
    - Inter-domain (AS) routing：AS 間的路由 → Exterior Gateway Protocol (EGP)
- Network Routing Entries ![](https://i.imgur.com/hDeFnjf.png)
    - administrative distance (AD)：Cisco 裡將不同的路由協定給一個數值
        - AD 數值表現路由協定 "trustworthiness"，越低越好
        - 如果到同一 dst 有兩種協定的路由，選 AD 較小的那一條
            |Route Source |Administrative Distance|
            |:---|:---:|
            |Connected |0|
            |Static |1|
            |EIGRP summary route| 5|
            |External BGP |20|
            |Internal EIGRP |90|
            |IGRP| 100|
            |OSPF |110|
            |RIP| 120|
            |External EIGRP| 170|
            |Internal BGP| 200|
    - metric 也是越低越好
#### Dijkstra’s algorithm (Link State)
- 讓每個router都有整個網路的拓譜資訊(net topology) ，收到每個node的相鄰資訊
- notation:
    - c(x, y)：x 到 y 的花費，如果不相鄰就 = ∞
    - D(v)：目前從 src 到 v (dst) 的最小花費
    - p(v)：目前從 src 到 v (dst) 的最小花費的路徑裡，v 的 predecessor
    - N'：包含所有已知有有限的最短路徑的點集合
- 演算法 ![](https://i.imgur.com/1Bp8PZF.png)
    - 先找沒被走過中擁有最小的邊的其中一端點，加入 N'
    - 取出所有連接此點的邊更新他們之間的距離，並拿出這些之中最小的邊(選擇走他)
    - 將被選擇的點再加入 N'，繼續更新他相鄰的邊，如果相鄰點的原本的距離比此點加上此邊的距離還常的話就更新他
    - 直到所有點都在 N' 為止
    ![](https://i.imgur.com/i3rygLC.png)
    - iterative：經過 k 次迭代，知道到達 k 目標的最小成本路徑
- 複雜度：n 節點
    - 每次 iteration：需要檢查所有不在 N' 裡的點
    - n(n+1)/2 次比較：O(n^2^)
    - 較有效率的實作：O(nlogn)
#### Distance vector algorithm (Bellman-Ford)
- d~x~(y) := x 能到達 y 的最小成本 ![](https://i.imgur.com/UfNKIEz.png)
    - Ex. du(z) = min { c(u,v) + dv(z), c(u,x) + dx(z), c(u,w) + dw(z) }
    - Dx(y)= estimate of least cost from x to y
    - x maintains distance vector Dx= [Dx(y) : y є N]

- 流程
    ![](https://i.imgur.com/xzmxWyx.png)
    - 一開始的 table 只知道到隔壁要多少
    - 每個點都要週期性把自己的資訊告訴隔壁，也會收到隔壁傳來的資訊
    - 如果有更改就看有無需要更新，若有更新就馬上把更新完的資訊傳給鄰居
    - 每個 local iteration 起因為來自鄰居的 local link cost change DV update message
    - distributed：(分散、去中心化)
        - 每個節點僅在其DV變化時通知鄰居
        - 鄰居然後在必要時通知鄰居
- link cost changes：
    - 節點偵測到 local link 花費變了，就更新並告訴鄰居
    - 鄰居收到新的資訊，如果 DV 更改，也告訴鄰居
    - **good news travels fast** ![](https://i.imgur.com/Z8wZSjl.png)
    - **bad news travels slow** → “count to infinity” problem！ ![](https://i.imgur.com/Zhb96F5.png)
        - 44 iterations before algorithm stabilizes

- 舉例：![](https://i.imgur.com/z4MFKdD.png)
- 算法收斂所需的最大迭代次數可以計算如下：在每次迭代中，網絡中的節點將與其鄰居交換距離表的信息。
    - 在第一次迭代之後，到當前節點的所有相鄰節點將知道到當前節點的最短路徑成本
        - 有 X、Y 兩節點，它們是鄰居
        - 然後，在第一次迭代之後，Y 的所有鄰居都會知道到節點 X 的最短路徑成本
    - 假設d（網絡直徑）是最長路徑的長度，並且網絡中**任何兩個節點之間都沒有迴路**
    - 根據上述類比，執行d-1迭代後，所有節點都將了解到d到所有其他節點的最短路徑成本
    - 如果路徑長度大於d跳，則路徑包含循環。循環的刪除將算法結果最多收斂到d-1次迭代
    - 跳數大於d的任何路徑都由循環組成，這些循環導致算法的結果最多收斂d-1個迭代。因此，距離向量算法的結果最多收斂d-1次迭代

| | LS | DV |
| --- | --- | --- |
| 複雜度| 每個節點都必須知道網路中所有連結的成本| 只須跟相鄰的節點交換訊息|
|收斂速度	| 實作是一個$O(\vert N\vert^2)$，需要$O(\vert N\vert \vert E\vert)$比訊息|	 若最長 hop 為 d，總迭代數需 d-1|
#### Routing Information Protocol (RIP)
- RIP 採用 Distance Vector ，以 hop 數來做為距離的判斷
- 缺點：如果有迴圈的話，他只會選比較 hop count 少的來決定，不會以速度來決定(不看 cost)
#### OSPF (Open Shortest Path First)
- 切多個區域，每個區域都有不同的規則 → 難
- Singal area：所有區域都一樣且都是0
    1. Establish Neighbor Adjacencies
    2. Exchange Link-State Advertisements (LSA)
    3. Build the Topology Table
    4. Execute the SPF Algorithm
    5. Modify the routing table
- 封包格式：![](https://i.imgur.com/mtbL55t.png)
    1. 放 Dst multicast 所有的 MAC 之一
    2. IPv4 dst address 包含 protocol 變數 → OSPF 為 89
    3. 標示 OSPF pkt type、router ID (用來表示不同的路由器，盡量先設，因為開啟的時候就會把它廣播出去，太晚設他就不會廣播出去)、area ID (分區塊進行)
    4. 依不同的類型放不同的內容
- 5 種封包
    1. Hello pkt：用於與其他 OSPF 路由器建立和維護鄰居關係
    2. Database Descriptor (DBD) pkt
        - 包含送端路由器的 Link-State Database（LSDB）的縮寫列表
        - 給收端路由器來檢查日期數據庫同步
        - 內容包含：Link type、advertising router 的地址、Link’s cost、Sequence #
    3. Link-State Request (LSR) pkt：用來請求有關 DBD 中任何條目的更多信息
    4. Link-State Update (LSU) pkt：用於答复 LSR 和宣布新信息
    5. Link-State Acknowledgment (LSAck) pkt：路由器發送以確認收到 LSU
- OSPF 會經過許多狀態以達收斂：
    - Down → Init state：發 Hello 封包到所有有 OSPF 介面出去
    - Init state：如果收到不是鄰居的 Hello 封包，就將她加入鄰居行列
    - Two-Way state：如果收到鄰居的 Hello 封包，就進入此狀態，然後開始交換其他四種封包來達成 synchronizing DBs
    - ExStart state：兩相鄰路由器會決定誰要先發 DBD 封包，ID 高的先發(僅決定順序)
    - Exchange state：依決定的順序互相發 DBD
    - Loading state：如果收到較新的 DBD，進入此狀態
    - Full state：全部完成
- Designate Router (DR) & Backup Designate Router (BDR)
    - DR election：依 priority、router ID 來決定高下
    - 擁有最高 priority 會當選 DR：為 0 – 255、預設 = 1、如果 = 0 代表不參選
        - 如果平手就是 ID 大的當選 (在每個介面上可能扮演不一樣的角色)
    - BDR 就是 DR 以外選出來最好的那個
    - 路由連到交換時，介面鄰居會變多個
    - DR 掛了之後，先讓 BDR 頂替，剩下的在選一個 BDR，再跟 DR 比一次，選出真正的 DR
    - pre-emptive (先發制人)：就比較容易當選，要另外開啟
- Loopback Interface
    - 永遠都會啟動的介面
    - 用來連他自己、讓與介面連接的裝置能連到他
#### Static route & Default route
- 沒有直接連上又沒有其他路由協定時，就要設 statcic route 才會通，2 種設法：
    1. 接 IP：就是下一個 HOP 的 IP
    2. 接介面：就是要出去的介面
    - 如果同一條兩種都下時，就會把兩個合併起來
    - 差異就是 routing table 會搜尋幾次
        - 接 IP 就會先拿到 IP，再去搜尋這個 IP 要從哪個介面出去，共 2 次
        - 接介面就直接可以出去，共 1 次
- 如果路由器只有唯一的出口(接路由器)，或者出口接很少，就直接設定 static route 就不用花時間跑 table (孤獨的網路，出去如果是國際的就不行這樣設)
    - Summary Static Route： static 和學習的一起用
    - Floating Static Route：當 static  壞掉時就用學習到的那一個
- routing table
    - S：手設的路由
    - C：顯示自己連到的地方(自己所在子往段)
    - L：顯示自己這台的 IP
- default route：static route 為 0.0.0.0/0，不管是誰都會被 match 到
### Access Control List (ACL)
- Wildcard Masking：把整個網段直接全部(擋掉 / 通過)
    - 0：**Match** 對應地址同位置的 bit
    - 1：**Ignore** 對應地址同位置的 bit
    - 若要擋奇數的IP → deny x.x.x.1 0.0.0.254 → 0.0.0.11111110
    - any 就是除了有規定的 IP 之外所有其他 IP
- Inbound ACL：ACL 會發生在查 routing table 之前 (過濾要進來的封包)
- Outbound ACL：已經查過 routing table 之後再決定要不要送 (過濾要出去進來的封包)
- 按照條目順序比對，比對到了就執行
- Standard ACL 大多用這個，1-100、1300-1999
    - 只看 src ip，放在離 dst 近的地方
    - 若放在離 src 近的地方，會導致他無法達到其他網段
- Extended ACL 進階ACL，101-199、2000-2699
    - 可以過濾 src、dst、協定種類、在哪個 port 上
    - established : 新進的不讓進，以前進過的就在讓她進
### Simple Network Management Protocol
- 預防勝於治療，五大需求(FCAPS)：Fault-management、Configuration、Accounting、Performance、Security
- 於應用層的 protocal (RFC 1157)，主要拿來管理網路設備 ![](https://i.imgur.com/NVeO0Dr.png)
- Network Management Stations (NMS)：用來管理的軟體，稱 SNMP Collector、Manager
- Network Elements：扮演管理者、被管的網路設備
    - Management Agents (SNMP Manager)
        - 可以執行 NMS 的命令，讓他去跟 agent 要，再由她回 MIB
        - 可以用 "get" 來收集 SNMP agent 的資訊
        - 可以用 "set" 來在 agent 上交換 configuration
        - SNMPv2c：可用 "GetNext" 來問下一個資訊
    - SNMP Agents
        - 若 manager 用 "traps"，可設定條件，滿足後就自動回報，就不用等他來問 → 減少處於 boring 的狀態
        - SNMPv2c：可用 "Inform" 來發送 ACK 給 SNMP Manager
- SNMP Protocol
    ![](https://i.imgur.com/dxWVEGR.png)
    - 定義如何於 SNMP Manager 和 Agents 間交換管理的資訊，不負責解讀 MIB 的資訊
    - SNMP Manager → SNMP Agents：**UDP port 161**
    - SNMP Agents → SNMP Manager：**UDP port 162**
- Management Information Base (MIB)：需另外用軟體去解讀
    - 儲存有關裝置的資料、operational statistics、user authentication
    - 保障兩邊交換的資料是有(標準)結構的 (固定形式以便判斷數值等等)
    - Standard MIB：每一家廠商的網路設備都有的物件
    - Private MIBs (extension)：某家設備獨有的物件
    - Structure of Management Information (SMI) (RFC 1155)
        - Defines the general framework for defining SNMP MIBs
        - 描述 **Managed Objects (MOs)** 在 MIB 裡如何被定義、可以擁有的 data types 和 values、如何被取名
        - Abstract Syntax Notation One (ASN.1) 用來定義 MIB-I 的 MOs：讓你去跨平台
        - RFC 1212 用來定義 MIB-II 的 MOs：現今最常用
    - SNMP MIB 只能儲存 simple data types
        - Scalars、2-dimensional arrays of scalars
        - MOs 就是階層結構的 rooted tree：葉子是 MOs，每個都有唯一的 Object Identifier (OID) 來分辨是甚麼的資訊 ![](https://i.imgur.com/K42CFmd.png) ![](https://i.imgur.com/npITWNt.png) ![](https://i.imgur.com/c4h61DJ.png)
        - 那麼多 entry 代表的其實是二維的表格，用一個序列來表示 ![](https://i.imgur.com/THQkUVa.png) ![](https://i.imgur.com/OfIFjrJ.png)
## Data-Link Layer
### Introduction
- Link 為相鄰節點的 communication channels
    | 角色 | 扮演者 |
    | ---- | ---- |
    | nodes | hosts、routers |
    | link | wired links、wireless links、LANs |
- 比較 
    |#|Layer|pkt name|Protocal|
    |---|---|---|---|
    |5|Application|message|HTTP, FTP, SMTP...|
    |4|Transport|segment|TCP, UDP → 程序間的溝通|
    |3|Network|datagram|Internet 協定 → IP → **Router**|
    |2|Link|frame|Ethernet 協定 → MAC  → **Switch**|
- datagram 在不同的 link 種類裡用不同的協定來傳遞
    - Ethernet → 有線、frame relay → LAN、802.11 → 無線
    - 個別提供不同的服務 (不一定有 Reliable Data Transfer)
- framing, link access
    - datagram 去 header(頭)、trailer(尾) 變成 frame
    - shared medium (共用的東西EX：switch) 的 channel access，因為沒弄好可能會碰撞 → 解決碰撞之後，錯開的機制是否公平
    - **MAC**(Medium Access Control) 為 frame 裡用的地址，每個製造商會先錯開，他再用流水號錯開
- 相鄰節點的 reliable delivery
    - we learned how to do this already (chapter 3)
    - 鮮少用到 low bit-error link：fiber、some twisted pair
    - wireless links：high error rates
- flow control：目前乙太是不做的，但可開啟
- 收送種類限制：
    - Simplex：只能單向
    - half-duplex：不能同時雙向
        - wifi：(是用震幅來判斷高低)，因為訊號的介質是空氣，同時收送的話，訊號會重疊相加，就看不出來正確的高低了
    - full-duplex：可以同時雙向
        - 乙太：裡面算四條線，兩條給收，兩條給送
        - 4G：因為是一個頻帶，它可以將頻帶切成多個頻道，有些拿來送，有些拿來收
- 網卡 **NIC** network interface card ![](https://i.imgur.com/NVS8Ld8.png)
    - combination of hardware, software, firmware(韌體，運作在 controller 上的程式)
    - Adaptors communicating ![](https://i.imgur.com/TzWXNdE.png)
        - 發送端
            - 封裝 datagram → frame
            - 增加 error checking bits、rdt、flow control
        - 接收端
            - 檢查 errors、rdt、flow control
            - 解 frame 封裝 → datagram，再傳給上層
### Error detection
- EDC= Error Detection and Correction bits (redundancy)
    D = Data protected by error checking, may include header fields
    - Error detection 並非 100% 可靠！
    - protocol 可能沒偵測出錯誤，但很少
    - 但若是 larger EDC field 會有比較好的 detection and correction ![](https://i.imgur.com/7KtG65u.png)
- 要先講好要用 even / odd  parity ![](https://i.imgur.com/sdTuwuQ.png)
    - 二維就可以直接知道哪個 bit 有問題由收端直接改掉即可 → error correction
    - 但要是連錯偶數個 bit，就無法偵測出是哪裡錯(但機率不高)
    - 但要偵測就需要傳送比較多的 bit，要付出相應代價
    - 如今並不通用，都直接使用 retransmittion
- Cyclic redundancy check (CRC)
    - 可看成 L2 的 checksum，是放在封包的後面 ![](https://i.imgur.com/nkeljqP.png)
    - more powerful error-detection：多攜帶同樣 bit 數，卻表現比較好
    - $\tt D$ 為 data 用 bits 來看，binary number
    - $\tt G$ choose **r+1** bit pattern (generator)，送收端都知道
    - $\tt R$ choose **r** CRC bits 滿足
        - <D,R> 必須整除 G (in modulo 2 → 相減時不用借位的算法)
        - 收端知道 G，把收到的 data 拿去除以 G，如果餘數不是 0 → error detected!
        - 可以偵測到所有小於 r+1 bits 的 errors 
    - 通用於 Ethernet、802.11 WiFi、ATM
    - $\tt all\ bit = D\times 2^r\ XOR\ R$
        - 先把向左移 r bits，移完後面那段會是 0，用 XOR 來將 R貼到後面 ![](https://i.imgur.com/BHedtY9.png)
### Multiple access protocols
- point-to-point
    - PPP for dial-up access
    - point-to-point link between Ethernet switch, host
- broadcast (shared wire or medium)
    - old-fashioned Ethernet
    - upstream HFC
    - 802.11 wireless LAN
- 如果是多個裝置要存取同一裝置，EX：wifi、MAC
    - 因為無法同時所以要特地去設計每個時間點下可用的分配規則
    - 用 distributed algorithm 決定節點如何分享 channel (節點甚麼時候可以傳輸)
- 理想狀態：
    - broadcast channel of rate R bps
    - 當只有單一節點在傳輸時，可拿到 rate R
    - 當有 M 要傳輸，每個點可拿 R/M，希望分配平均
    - fully decentralized：(不要有中控來控制)
        - 不要有特殊的節點來主控大家
        - 不要同步時間(太麻煩)
        - 因為如果這台掛了就會讓整個系統癱瘓
- MAC protocols：taxonomy (分類) → 共三種作法
#### Channel Partitioning
- 把 channel 切成小塊 (可依照 time slots、frequency、code)，做不同的作用
- TDMA (time division multiple access)：依**時間**切割
    - 每個周期內每個 slot 都會固定會分配到一段時間(= packet transmission time)是專門給他傳送，他如果不傳就空著
    - 缺點：沒有達到最大使用率、會延遲 (因為要等下一輪)
    - EX：6-station LAN、1,3,4 have packets to send、slots 2,5,6 idle ![](https://i.imgur.com/xQIwMvD.png)
- FDMA (frequency division multiple access)：用**頻率**切割
    - 每個人有自己的頻道，沒用的就空著
    - EX：6-station LAN、1,3,4 have packet to send、frequency bands 2,5,6 idle![](https://i.imgur.com/j6MPXAv.png)
    - EX：手機講電話時，要保證好的通話品質，那你不講是你的損失
    - 優：保證傳輸品質，缺：沒有達到最大使用率
- 效率：
    - high load：公平、有效率
    - low load：效率低、delay in channel access、單點傳輸也只能拿到 1/N 頻寬
#### Random Access
- 並沒有切割 channel，且允許 collisions → 要修復碰撞
    - 頻道都是滿的 rate R (除非大家都不送)
    - 節點間沒有 prioricoordination (事先協調)
- 需要的能力：
    - 要有能力偵測碰撞
    - 如何修復碰撞，重送不加一點延遲可能再撞一次
- Slotted ALOHA![](https://i.imgur.com/xNPMylq.png)

    - 夏威夷的人發明的，因為島多通訊要用，把封包打到衛星，再打下去，可突破中間有海的地理限制
    - Assumptions：
        - frames 大小相同，時間也切成相同大小，節點是 synchronized (同步的)
        - 只有在一個 slot 開始的那一刻才能開始發送封包，與窗格對齊
        - 如果 2 個以上的節點在同 slot 傳輸，所有節點都偵測到碰撞
    - Operation：
        - 如果節點觀察到 fresh frame，在下個 slot 送
        - 沒碰撞：下個 slot 也可以送封包
        - 碰撞：要重送，用機率來決定自己要不要在下一個 slot 重送(如果大家都在下一次重送的話會再撞一次)
    - 優點：
        - 如果只有一個點要送，就可以持續佔滿它
        - highly decentralized(去中心化)：只有 slot 要同步，其他不用 (同步的項目少 → 簡單)
    - 缺點：
        - collisions 可能造成 idle slots 浪費、校正時間不好做
        - 節點需要用比傳送封包還要少的時間去 detect collision
    - 效率：
        - 假設有 N 個有很多 frame 要送的節點，碰撞後決定下次送的機率為 p
        - 自己要送成功的機率 = p(1-p)^N-1^
        - 有一個點成功的機率 = Np(1-p)^N-1^
        - Max Efficiency：找到一個 p' 使 Np(1-p)^N-1^ 為最大值
        - N → 無限，Np'(1-p')^N-1^ → $\tt max\ efficiency = 1/e = 0.37$
        - 頻道有 37% 時間是被有用的傳輸佔用
- Pure (unslotted) ALOHA
    - when frame first arrives 想送就送、較簡單、非同步化
    - collision 機率增加：在 t~0~ 送的訊框會跟在 [t~0~-1, t~0~+1] 傳送的封包碰撞![](https://i.imgur.com/2D0Tp3x.png)
    - 效率：比 slotted Aloha 還糟
        P(自己成功) 
        = P(傳輸機率) × P(沒有其他人在 [t~0~-1, t~0~] 傳送)× P(沒有其他人在 [t~0~, t~0~+1] 傳送)
        $\tt = p \times (1-p)^{N-1}\times (1-p)^{N-1}$
        $\tt = p \times (1-p)^{2\times (N-1)}=$ (N → $\infty$) $\tt 1/2e = 0.18$
- CSMA (carrier sense multiple access)
    - 傳輸前先聽：idle → 傳輸、busy → 延遲傳輸 (不要在講話的時候講話)
    - collision：整個封包的傳輸時間都浪費掉
        - distance & propagation delay play role in in determining collision probability
        - 就算有先聽再送，還是會因為傳遞延遲(propagation delay)而導致你以為沒人在講話而講話，造成碰撞
        - 若要偵測碰撞：邊送邊聽，如果沒碰撞，邊聽的時候應該要聽到自己所發出的封包
        - 因為無偵測碰撞功能，所以還是堅持送完 → 浪費
- CSMA/CD (collision detection)
    - 加入偵測碰撞功能 (知道跟別人同時講話就不要再講了) ![](https://i.imgur.com/IB7GXds.png)
        - 在短時間內偵測碰撞，偵測到就馬上停止傳輸，減少浪費
        - 有線 LAN：因為訊號不會減弱，容易比較聽到的和自己傳出去的是否相同
        - 無線 LAN：因為訓好強弱差很多，很難比較
        - 在用一個機率來定要甚麼時候聽 (把 sence channel 也錯開)
    - Ethernet CSMA/CD 演算法
        1. NIC 收到網路層的 datagram → 封裝成 frame
        2. 如果 NIC 偵測到 idle → 開始傳送 frame，若沒有則等到 idle 再傳
        3. 如果沒偵測到其他在人搶就會全部傳完
        4. 如果遇碰撞就停止送，然後再多傳幾個位元給別人(怕別人沒偵測到碰撞)
        5. 停止之後，NIC 進入 binary (exponential) backoff 狀態
            - 在 m^th^ 碰撞後，NIC 在 {0,1,2, …, 2m-1} 裡隨機選一個 K
            - NIC 會等 K×512 bit times 才會返回 2.
            - 如果連續撞，下一次就會等更久(TCP 也是設計成越等越久)失敗超過一定次數就會 fail → 不送了
    - 效率：
        - T~prop~ = 兩節點間的 max prop delay
        - t~trans~ = 傳送 max-size frame 所需時間
        - $\tt efficiency=\frac{1}{1+5T_{prop}\ /t_{trans}}$
        - $\tt efficiency→1$ 時 $\tt T_{prop} → 0,\ t_{trans} → \infty$
        - 較簡單、較便宜、去中心化、效率佳
- CSMA/CA (Collision Avoidence)： (wifi 在用)
    - 訊號強弱差太多沒辦法比，無法偵測碰撞 → 改成碰撞避免機制
    - carry sense：訊號傳遞範圍有限，要先聽也聽不到，且可能造成浪費
    - 送出資料前，聆聽網路上的狀態，如果沒有人使用，維持一段時間後，再等待一段隨機的時間後如果還沒有人使用，才送出資料。由於每一個裝置採用的隨機時間不同，可以減少碰撞的機會
    - 送出資料前，先送一個RTS (Request to Send) 封包給目標端，等待目標端做出回應有就是送出 CTS(Clear to Send) 封包後，才開始傳送
    - 有人要送封包出來時，先送一個含 RTS (request) 的封包給大家，收到的人就在這個時間內閉嘴
    - 有人已經聽到別人的封包時，廣播一個含 CTS (clear) 的封包，讓大家知道有人發東西來了，叫大家閉嘴
    - 可重送 4 / 7 次，超過就 drop，也有 ACK 機制
- 效率：
    - efficient at low load：單點可用滿整個頻道
    - high load：collision overhead
#### "Taking Turns"
- polling：
    - master 輪流 "邀請" slave 來傳遞封包
    - 通常跟 "dumb" slave 裝置一起用
    - 缺點：
        - polling 花費、latency(延遲)
        - master 掛掉：設一個 timeout，如果太久沒人過問，就先假設 master 掛了，用演算法選出下個 master
- token passing (權杖)：
    - 大家輪流拿 control token，拿到才能發東西出來
    - 缺點：
        - token 花費、latency(延遲)
        - token 消失時：
            - 設 timeout，很久沒收到就當他不見了，就自己造一個權杖放回網路
            - token 的碰撞：也要用演算法舉行選舉，看要用誰 token
        - 還要加上 token pkt transmission time，如果中間都沒人要送，就要等他繞一圈回來才能送
    - 優點：很公平、token 本身幾十 bytes 而已，占全部的資料傳輸空間也不多
    - high load：運用率很高
    - low load：沒有要發也只是把權杖給下一個而已
- Bluetooth, FDDI, token ring
- 效率：綜合前兩者的優點
### MAC address
- `ifconfig` 來查看介面上的資訊，`em0, em1`為 em 這個廠商的第 1, 2 張網卡，不同廠商有不同的開頭
- 48-bit MAC：為 6 * 2 個 16 進位的數字組成，中間用 "`:`" 來分隔，EX: 12:36:3d:8a:3b:c1
- Flat address：刻在卡上拿到哪裡都不會變，可帶去別的 LAN (但要跟別人重新要IP)
- broadcast : FF-FF-FF-FF-FF-FF(48bit 都是1，只能廣播自己的LAN)
- 網卡只收3種封包
    1. Unicast 以自己為目的地 mac
    2. Multi-cast 有加入的 1 對多
    3. Broadcast 廣播 
    - 監聽是要改成 promisculus mode 就可收所有封包 EX.wireshark (無法監聽 wifi 的封包)
- 不同的 interface 有不同的 table、MAC (面對不同的LAN)
### ARP (address resolution protocol)
- 用於MAC和IP轉換 ![](https://i.imgur.com/ey0pR39.png =150x100)
- 每個 IP node (host、router) on LAN 都有 ARP table
- IP/MAC 對應其他人：< IP address；MAC address；TTL>
- ARP “plug-and-play”：會自己完成，不須手動每個去設定
- 發生在LAN的行為，乙太內的 MAC 和 ARP 裡的 MAC 會填的不一樣
- 封包格式：包在ethernet的標頭裡面![](https://i.imgur.com/1YghLSY.png)
    - 發封包還沒回覆時先在目標MAC填0、A 要跟 B 建連線
    - 順序：src-ip、src-mac、dst-ip、dst-mac
    - request 封包：A-ip、A-mac、B-ip、00:00:00:00:00:00 
    - reply 封包：B-ip、B-mac、A-ip、A-mac
    - if 中間會經過 router 會先問他的 MAC，他在去問下一步的 MAC
    - if 是透過 ARPproxy server，mac 會是收到的 server 的同一面的mac位址
- 流程：![](https://i.imgur.com/QXeW9gn.jpg)
    - 當 A 想傳封包 (datagram) 給 B 時，只有 IP 卻沒有 MAC，就發 ARP 來問
    1. 先找 cache 裡有沒有他要的 ? 直接連線 : 執行2.~4.
    2. srcHost broadcast ARP request 封包 (dst = FF-FF-FF-FF-FF-FF): 通知LAN裡所有主機看誰是他要找的
    3. dstHost 回 ARP reply 封包 : 告訴src自己的MAC (非目標就會把此包discard)
    4. 加入 ARP table (視為 cache，直到 TTL timeout 才刪除)
        - Soft state：一直送封包 → 用此達到 keepalive
        - TTL (Time To Live)：得到的 MAC 資訊還有多久要被忘記 (通常 20 min)，中間有傳輸就reset
- send datagram from A to B via R(路由器)![](https://i.imgur.com/dnRfPJj.png)
    - 格式：src-ip、src-mac、dst-ip、dst-mac
    - A → R：A-ip、A-mac、B-ip、R-mac (A gateway)
    - R → B：A-ip、R-mac (B gateway)、B-ip、B-mac
    - ![](https://i.imgur.com/WmYb8OM.png)
    - ![](https://i.imgur.com/2ymCA0l.png)



### Ethernet
- "dominant" 主宰 wired LAN 技術：
    - single chip、多種速度、簡單、便宜
    - 最早廣泛使用的有線 LAN 技術
    - 速度：10 Mbps –10 Gbps
- 乙太拓樸![](https://i.imgur.com/Jd3g85E.png)


    - bus：popular through mid 90s (過時)
        - 傳遞訊號時會到同一條線上 → 碰撞
        - 同時間只能有一個傳輸在進行
    - star 星狀拓樸：現今仍在使用
        - switch 當中心點，還可以增加 throughput (可同時進行)
        - 訊號到交換器就會停下來，並不會發生訊號碰撞的問題
            → CSMA/CD 根本就不需要了，直接一直猛送就行
        - 但還是有可能在 buffer 掉封包，但送端不會知道 → 需依靠 TCP 的重送
- header (802.3 Frame) ![](https://i.imgur.com/J56rHgL.png)
    - **preamble**：8 bytes
        - 原本都傳 10101010... (7 bytes，用來達成同步) 直到出現 10101011 就代表下一個 bit 開始是地址的部分，preamble 部分結束
        - 要把 bit time 的時間間隔講好，難在同步 clock rates
        - 物理上用高低電壓，他會在每個 bit time 去偵測電壓來判斷是 0 或 1，但如果沒對在波的中間(高峰，實際上的波不會是方波而是曲線波)，他就可能把 1 對到 0
         ![](https://i.imgur.com/51POawg.png)

        - 所以其實封包不是送到的那瞬間全部收到，還是一個個位元依序收，收完才收到的
        - $Q$：為何 WIFI 的速率要一直改？
            $Ans$：因為bit error率與傳送速率成正比，傳送速率 = 1/bit time，當 bit time 越短，他去偵測會因為她還沒昇或降電壓而測到錯誤值，所以錯誤率越大 → 所以當錯誤率大時，降速來提升準確率
    - **addresses**：6 byte src、dst MAC
        - 如果 adapter 收到 dst mac 是自己的或廣播 mac，才會解封裝傳給上層，否則丟棄
    - **type**：表示上層是哪個協定，通常是 IP，但也有其他的 EX. Novell IPX、AppleTalk
    - **CRC**：收端會 cyclic redundancy check，若有出錯就丟棄
- 特色：
    - connectionless：不須 handshaking，要送就直接送
    - unreliable：收端 NIC 不會回送 acks 或 nacks → 用高層協定來修復
    - 運用 unslotted CSMA/CD with binary backoff
### Ethernet switch
- link-layer 裝置：
    - store & forward Ethernet frames
    - 溝通通常在同一個LAN，24/48 port
    - 檢查收到的封包是否要去的是 LAN，不是的會就送給預設閘道
    - 是的話就送到他該去的地方
    - transparent：hosts 是不知道交換器存在的
    - plug-and-play、self-learning：插上網路線就可以用，不用設定就自己完成
- 自我學習 (MAC learning)：
    - 在哪裡收到 A 的資料，他就在哪個 interface，將她的 MAC 寫進表裡
    - 如果不知道目的地在哪裡，就對 A 以外的介面 unicast (flood) = **selected forward**
        - 選擇性傳送到 1 個或多個 link
    - 透過傳送接收來不斷填滿table，而知道大家的位置，時間(TTL)到了會清
    - if 多階也可以學習再沿路回去
    ```c
    if(entry found for dst){
        if(dst is the place where its come from) drop frame
        else forward frame on interface indicated by entry
    }
    else flood // forward on all interfaces except arriving interface 
    ```
- **Router vs. Switch**
    |VS.|Router|Switch|
    |------|------|------|
    |Layer|Network (Datagram)|Link (Frame)|
    |forwarding table|compute|learn|
    |所使用方法|routing algorithm, ip|flooding : 不知道送哪就選擇性全部送<br> learning, MAC address|
### VLAN (Virtual LAN)
- LAN：不需要路由的區域
- 作用：![](https://i.imgur.com/JHP4A0X.png)
    - 在實體網路用邏輯等切成幾個不同的 LAN，但物理上是同一個
    - 用 L2 的方法把 LAN 切成多個 broadcast domain → L2's VLAN
    - 是一個邏輯的連線，而不是實體的連線
#### IEEE 802.1Q (Frame)：
- 最常見/經典的 VLAN protocal
- 定義：如何在 headers 裡打上 tag、碰到tag如何反應作用
- 在 switch 打上 tag (4bytes) 來表示是哪個 VLAN![](https://i.imgur.com/iqes8RM.png)
    - **Type**：(4-byte) 包括 Tag Protocol Identifier (TPID)、Tag Control Information (TCI)
    - **TPID**：(2-byte) 
        - VLAN：0x8100、ARP：0x0806、IP：0x0800
        - 如果看到0x8100而且認識，會直接繼續解讀後面 VLAN 的資料
    - **TCI**：(2-byte)
        - **User priority**：(3-bit) 可以讓有標籤的訊框攜帶優先權資訊通過無法支援優先權的網路 （如Ethernet），優先權的範圍為 0 ~ 7
        - **Canonical Format Identifier (CFI)**：(1-bit)
            - CFI = 1 表示此標籤標頭中包含 RIF 欄位，而且 RIF 中的 NCFI 旗標值決定訊框資料中所攜帶的MAC位址是「制式格式」 (Canonical format) 或「非制式格式」(Non-canonical format)
            - CFI = 0 則表示此標籤標頭中不包含RIF欄位，而且訊框中所包裝的MAC位址都是「制式格式」
            - 這裡所謂的「制式格式」是指一個位元組的位元在網路上傳送的順序。如果最高位元 (most significant bit) 先傳送，則稱為「制式格式」，相反的，如果最低位元 (least significant bit) 先傳送，則稱為「非制式格式」。
        - **VLAN ID (VID)**：(12-bit) 1 ~ 4096
- 如果無法處理 VLAN 的裝置還是可以接收此封包，只是會把它丟掉
#### VLAN-aware Network：![](https://i.imgur.com/ivNJKPs.png =350x120)
- 進入時會打上 tag，出去時拿掉，一台中間的可以連接多個 VLAN
- 可在這裡面流通卻不會打 tag 就是 native VLAN → 不上標籤的例外 (預設 VLAN 1)
- Default VLAN：
    - 通常是 VLAN 1、開機就會存在
    - 所有 L2 的控制都跑在這個 VLAN 上
    - 如果不是我們設定的，就是預設VLAN
    - 通常是拿來管理自己的IP的，所以希望大家都能收到他
    - 所以只要遇到 native VLAN 就會幫她剝掉 (VLAN1 可以送到任何VLAN，因為都會幫忙剝掉)
- Data VLAM：用來切割這些電腦的 VLAN、拿來將電腦分群
1. untagged (access) port：
    - 從外面進來 (in)：打上此 port 所設定的 VLAN tag
    - 從裡面出去 (out)：如果此封包的 tag 符合此 port 的 VLAN #，就幫他剝掉
    - 也有學習的功能(學MAC address)，像原始的switch
2. tagged (trunk) port：
    - 從外面進來 (in)：如果此封包的 tag 符合此 port 的 VLAN #，就讓它進來
    - 從裡面出去 (out)：如果此封包的 tag 符合此 port 的 VLAN #，就幫他傳出去
    - 等於出去也是 tagged，所以不會剝掉，設定過濾標籤，就可以達到 access control
    - 如果已有 tag 就不會改他，如果不符合的就丟掉
    - 如果收到沒有 tag 就把它當成 native VLAN(VLAN 1)，出去還是不會幫他加上去
    - 兩頭的vative VLAN要設一樣不然會搞混，也會學，但是是學 VID
- 一個 switch 進出的 port 都有不同的 config
- Example![](https://i.imgur.com/RRhXRKW.png =300x60)
    - S1-1, S2-2 untagged, S1-2, S2-1 tagged, All configured with VLAN 10
    1. A 送無tag的封包給 B
    2. Switch S1 收到無tag的訊框 from untagged Port 1
        - S1 加 VLAN 10 tag 再送去 Port2
        - Port 2 可讓 VLAN 10 通過，由 S1 → S2
    3. Switch S2 收到有 VLAN 10 標籤的訊框 from tagged port 1
        - Port 1 allows VLAN 10，讓它進來並決定讓他去 Port 2
        - port 2 是 untagged port，又符合 VLAN，幫她拔掉在送出去
    4. Host B 照常收訊框，毫無被貼撕標籤的感覺
#### VLAN 間的 routing → Inter-VLAN routing
- 涵蓋 L2、L3，還是要 gateway
- Legacy inter-VLAN routing  ![](https://i.imgur.com/ibfXmFo.png)
    - 每個 VLAN 都有一個介面，分別連接到不同的 switch 的 port
    - 利用路由器到交換器的兩條線來區別 vlan，dst IP 為 gateway
- Router-on-a-Stick ![](https://i.imgur.com/Kacc4L7.png)
    - VI 放在路由器上，中間用 trunk 連接，減少線數、port 數
- Layer 3 switching via SVIs (Multilayer Switching) ![](https://i.imgur.com/7c9ivdF.png)
    - 可執行基本的 routing，做起來比較路由器快
    - 交換 VLAN 不是用演算法，管理者 config 就可以做到
    - Switch virtual interface (SVI)
        - 每個 VLAN 把某個 SVI 當成default gateway
        - 進來是 trunk port，一個 port 就可以接收很多VLAN
- vty 只支持 extended vlan
### STP (Spanning Tree Protocal) (802.1D)
- 沒有 STP 的三種下場
    - database instability：MAC 對應表一直改變，因為從不同埠收到相同來源的封包
    - broadcast storms：因為如果收件者不是自己就會幫她傳下去，結果就是大家一直來回傳，switch 形成一個圈，然有有任一台發封包，然後此 dst 不再 arp 表裡，就會 flood 出去(兩邊)，然後就互相 flood，因為一直有不同來源的封包一直來，他就一直改變 table 裡的 MAC 所以又一直往別的地方傳，就視同一個交換器從不同的 port 收到同個 IP 的封包，他就會很清楚這個 IP 的位置
    - multiple frame transmission：因為是迴圈，往兩邊送，另外一邊也會送到，導致 dst 收到 2 個以上相同的封包
- Algorithm：
    - switch 內部把重複的路徑擋掉 (不拆線是因為哪天線壞了可以馬上換一條)
    - BDPU：屬於L2的控制訊息
    - 有問題時，重新計算路徑，重新擋 port
    - STP 速度較慢，所以才有 RSTP (快速STP)
    - ![](https://i.imgur.com/9601IMp.png =200x100) **→** ![](https://i.imgur.com/QppKOVC.png =150x100)　　![](https://i.imgur.com/OVrITje.png =150x100)
    - **選出 Root Bridge**
        - 所有 swItch 交換 BDPU (上面有權重，找出最小的 bridge ID)，就是 root bridge
    - **非 Root Switch 決定 Root Port**：每台一個，擁有到 Root Bridge 成本最少的路徑
        - 只有 Root Bridge 沒有 RP，直接連接到 Root Bridge 的那個埠都是 RP
    - **每條 Link 決定其中一端作為 Designated Port**：依交換的 BPDU 來決定
        - root bridge 上每個埠都是 DP
        - 如果 link 的一端是 RP，另一端一定是 DP (相反不一定)
        - 如果每一個 link 上都有一個DP時，要轉換的時候會比較快
        - 每一個 DP 到 Root 橋接器的距離是基於收到 BPDU 中的設定值，並加上下列的比較計算出來
        - 第一優先：比較 root path cost 的值
            - 各橋接器在轉送 BPDU 的時候，會將封包中 root path cost 值加上設定的 path cost。 因此 root path cost 值即是各個埠到 Root 橋接器的總和
        - 第二優先：root path cost 相同的話，則比較 BID
        - 第三優先：若是 BID 相同時(每一個埠都連接到相同的橋接器)，則比較 DP ID
            - 前 2 byte：連接埠優先權、後 2 byte：連接埠編號
    - **暫停使用 Blocking Port**
        - 每條 link 上只會有一端是 BP(BLK)，另一端就是 DP(FWD)
        - 可以收 BPDU 但不能送任何封
- 共 5 狀態：![](https://i.imgur.com/e4i1wQ9.png)
    - DISABLE：無效連接埠，忽略所有接收到的封包
    - BLOCK：僅接受 BPDU 封包
    - LISTEN：接受及傳送 BPDU 封包
    - LEARN：接受、傳送 BPDU 封包及學習 MAC 位址
    - FORWARD：接受、傳送 BPDU 封包、學習 MAC 及訊框的傳送
- 有包含 VLAN 的 STP (by Cisco)
    - Per-VLAN Spanning Tree (PVST)：STP adding the VLAN feature our STP
        - VLAN 單獨改變不會影響整棵樹，一個 VLAN 自己一棵樹
    - Per-VLAN Spanning Tree Plus (PVST+)：improved PVST
    - Rapid-PVST+：快速的 PVST+
    - MSTP (Multiple Spanning Tree Protocol) (not Cisco) 
        - STP 和 RSTP 的擴展，用於有 VLAN 的網絡
        - 最初定義 IEEE 802.1S 為 802.1Q 的修訂版，最後被合併為 IEEE 802.1Q-2005
#### RSTP (Rapid Spanning Tree Protocol) (802.1W)
- 演算法是同一個，只是記住了一些狀態，可以較快收斂
- 有三狀態：
    - Discarding：被 BLK 掉，只可收不能送
    - Learning：能傳資料的時候才會學習
    - Forwarding：可以收也可以送
- 一個機器一開始加入時會經歷 blocking → listening → learing → forwarding
- RSTP 還會把這種 port 儲存成三種狀態![](https://i.imgur.com/9xysPKM.png)
    - Alternate Port：普通可以收 BPDU 的 blocked port
    - Backup ports：可以收同一台 bridge 的 BPDU 的 blocked port，當兩條接到一樣時
    - Disabled ports：shut down 的 port
- 比較![](https://i.imgur.com/dnEciV4.png)
#### BDPU (Bridge Protocol Data Units) (802.3 Ethernet)
- 因為802.3所以沒有ethernet type![](https://i.imgur.com/IvqvutU.png)
    - Length <= 1500 802.2 LLC (??? Logic Control)
    - Length ≥ 1536 802.3 Ethernet II
    - 802.3 header 標示 src 和 dst of BPDU frame
        - Source：a unique MAC address from its origin port
        - Destination：a multicast address as destination MAC for the spanning tree group
- Bridge ID (BID) 是由 switch 的 Priority Value、Extended System ID、MAC Address 組成![](https://i.imgur.com/k2LIMWA.png =250x100)![](https://i.imgur.com/3iY2lq6.png =330x100)
    - Bridge Priority：自動設定的，但可以被更改
    - MAC address：送端 switch 的 MAC
    - Extended System ID
        - VLAN ID 或  multiple spanning tree protocol (MSTP) instance ID
        - proiority 要是4096的倍數，因為在extended Id (12bits) 前面
### Virtual Private Network (VPN) ![](https://i.imgur.com/UA356DT.png)
- Tunnel：不用管路由，就用隧道直達，很像兩者直接相連，有加密的連線
    - 把一 protocal 包在別的 protocal 裡面，然後就像兩個網路接起來一樣
    - EX：把 L2 的封包整個包在 UDP 裡面、IPv4 包在 IPv6 裡面![](https://i.imgur.com/il4PVFT.png)
    - Point-to-Point Tunneling Protocol (PPTP) [2637] ![](https://i.imgur.com/siI8Wn3.png)
        - Point-to-Point Tunneling Protocol (PPTP)：PPP + encryption + enhanced GRE
        - Layer Two Tunneling Protocol (L2TP)：PPTP + L2F
        - Generic Routing Encapsulation (GRE)：
            - 多加一個 header 在 inside、outside IP 中間
            - enhanced 版：提供 flow 和 congestion control
- Remote Access Over the Internet ![](https://i.imgur.com/2HegnDk.png)
- Connecting Networks Over the Internet (Site to Site VPN) ![](https://i.imgur.com/FjqIvIj.png)
- Connecting Computers over an Intranet ![](https://i.imgur.com/mhgmyU6.png)
### Security
- Common LAN Attacks on Layer 2
    - 拿到控制權
        - Cisco Discovery Protocol (CDP)：cisco 專有，通用的是 LLDP
        - Telnet Attacks
    - 癱瘓網路
        - ARP Spoofing、VLAN Attacks、DHCP Attacks
        - MAC Spoofing and Address Table Flooding Attacks
#### Cisco Discovery Protocol (CDP)
- 廣播為 periodic、unencrypted、unauthenticated
- 解決：使用者端其實不需要連上去(擋掉)、改成有加密的模式
#### Telnet Attacks
- 天生不安全，攻擊者可能利用 Telnet 獲得對 Cisco 網絡設備的遠程訪問
- **Brute Force Password Attack**：密碼設太簡單被暴力破解
- **Telnet DoS Attack**：攻擊者不斷請求 Telnet 連線，以試圖使 Telnet 癱瘓，以阻止管理員遠程訪問 switch
- 解決：增加安全性
#### ARP Spoofing
- 一種 man-in-the-middle 攻擊，也稱作 ARP poisoning
- 攻擊者發送包含偽造 MAC 的 ARP 封包
    - "中毒" 受害者的 ARP 緩存表會包含錯誤的 IP-to-MAC  mappings
    - 要送給該 IP 的任何流量都發送給攻擊者
    - 攻擊者可能會攔截網絡上的封包，修改流量或停止所有流量
    - 自己送封包 → 更改對應表，但有時候這樣做是為了好的用途
    - 但壞人會利用這個來收本來收不到的封包或讓別人收不到封包
- 解決：Dynamic ARP Inspection (DAI)
    - 檢查 ARP 的封包，把所有這類的封包攔截下來，檢查是否是有效的 ARP
    - DAI 的運作
        - 攔截所有 ARP 的 requests、responses
        - 驗證攔截的數據包是否具有有效的 MAC-to-IP bindings
        - 丟棄無效的 ARP packets
    - 需要一個 trusted database 來存儲有效的 MAC-to-IP bindings
        - Built at runtime by DHCP snooping (explained later)
    - Switch ports 預設為 untrusted
        - 連接到 hosts 的 ports 設為 untrusted，因為會有其他人連上來，所以要特別檢查
        - 連接到 switches 的 ports 設為 trusted，因為確定不會有人動手腳，就可以不用檢查 ARP 封包
#### MAC Spoofing
- 更改網絡面的 factory-assigned MAC 地址的技術
- MAC Spoofing Attack
    - 嗅探網絡以獲取有效的 MAC 地址，並更改其 MAC 地址以使其成為有效 MAC 地址之一
    - 繞過 servers、routers 上的 ACL...等
- MAC Address Table Flooding Attack
    - 送很多 ARP 封包，傳把 CAM Table 佔滿，佔滿後會進入 fail-open mode
        - Switch 廣播所有封包給所有 LAN 裡的裝置
        - 攻擊者就可以拿到所有的封包 → 更慘
    - 解決：開啟 port security
#### VLAN Hopping
- 欺騙 switch 讓他幫你傳遞不同 VLAN 間的訊息 (all through Layer 2 switching)![](https://i.imgur.com/ty8waNS.png)
- 解決：改 native vlan #、強迫 native vlan 上 tag
#### Two types of DHCP attacks
- DHCP Spoofing attack
    - 偽造假的 DHCP server 讓他發 IP 給 clients，讓他拿到錯的 DNS、gateway
- DHCP Starvation attack
    - 一直跟 DHCP 發 discover 封包 (且不斷換 MAC)，讓他一直發 IP 發到完
    - Denial-of-Service (DoS) attack：
        - 用非法流量超載特定設備和網絡服務，從而防止合法流量到達那些資源
        - 讓真正要用的裝置沒 IP 可要，使它用不了網路
- 解決
    - DHCP Snooping 有 2 種 ports，預設是 untrusted
        - Trusted Ports：連接到上游 DHCP servers 的 ports，可收 DHCP 的封包
        - Untrusted ports：連到 hosts 的 Ports，不應該收到 DHCP 的封包
    - 可開啟 DHCP Option 82 for port security
        - 又名 Agent Relay Information Option 或 Agent Information Option (RFC 3046)
        - 允許 DHCP relay agent 標示自己和原發送 DHCP 的 client
        - 可以成為 DHCP relay agent 的裝置：switch、router、firewall、server...等
        - 他就只會接收帶上選項的封包![](https://i.imgur.com/u31NeyK.png)
        - 運作![](https://i.imgur.com/cGuemYK.png)
        - Suboption ![](https://i.imgur.com/8tv2GA7.png)![](https://i.imgur.com/7GBPQdR.png)![](https://i.imgur.com/cEeRtQH.png)
            - Circuit ID：標示收到請求的 port or VLAN![](https://i.imgur.com/bGgw7dc.png)
            - Remote ID：![](https://i.imgur.com/j4DEM92.png)
                - 標示 DHCP Relay Agent 的 hostname 或其他描述
                - 預設為 switch 的 MAC address
### EtherChannel (Link Aggregation)
- 讓物理上多條線變成邏輯上的一條線(不會被 STP 擋)，讓頻寬變大![](https://i.imgur.com/ep2h2a2.png)
- 特性：
    - Fast 和 Gigabit 不能混用，要同一種
    - 兩端的數量、VLAN...等設置要一樣
    - 最多 8 條一組，Cisco 接收最多 6 EtherChannel
- 2 Negotiation Protocols ![](https://i.imgur.com/i1JYlZ6.png)
    - **Port Aggregation Protocol (PAgP)** (Cisco 專有)
        - On：沒啟用
        - Auto：只會回應收到的 PAgP，另一端要是 Desirable 才會運作 (預設)
        - Desirable：會主動發 PAgP，也會回應
    - **Link Aggregation Control Protocol (LACP)** (IEEE 802.3ad)
        - On：沒啟用 (預設)
        - Passive：只會回應收到的 LACP，另一端要是 Active 才會運作
        - Active：會主動發 LACP，也會回應
### First Hop Redundancy Protocols (FHRP)
- 第一個 hop 會是 default gateway，此協定就是讓他有備用 gateway
- 平常設定只能設定一個閘道
- 作法：
    - 兩個 gateway 聯合騙 client 只有一個閘道，形成一個 virtual gateway，對外溝通都用這個虛擬閘道 (有 virtaul ip 和 MAC)
    - 一個是 forwarding router，一個是 stand-by router![](https://i.imgur.com/k8kDgwC.png)
    - 所以他們會一直交換封包，如果 standby 很久沒收到 active 的封包，就覺得它掛了，然後取代它的位置![](https://i.imgur.com/zEQlMRn.png)
    - 其實可以大於兩個，剩下的就是 listen router，當 standby 取代了原本的 active，就會有一個 listen 變成 standby
- 可用協定：HSRP、VRRP、GLBP
#### Hot Standby Router Protocol (HSRP)
- A CISCO proprietary protocol, which provides redundancy for a local subnet.
- HSRP group
    - 每個 group 都有一個有 MAC addr、IP addr 的 virtual router
    - 其中包含 1 個 Active router、1 個 Standby router、0 個以上的 Listening router
    - 服務不同的人，會有 group ID
    - Hosts 要將 virtual router 設成 default gateway
    - 只有 Active router 負責當 virtual router
    - active 掛了由 standby 接手
- Priority：選舉中用來決定誰是 Active router
    - HSRP priority 為 0 ~ 255，預設為 100
    - 由最高 priority 當 Active router
    - 如果 priority 相同，則擁有較高 IPv4 address 當 active
- Preemption
    - 預設如果一個 router 變成 active router，除非壞掉不然都不會換人，就算有一個較高 HSRP priority 的路由器上限也不換人
    - 開啟 preemption 強制重新舉行 HSRP 選舉，以保證最高 priority 的人當 active router
    - 如果沒有開 pre-emption，第一個開機的 router 就會變成 active router (如果沒有其他路由器開這要一起選舉)
    - 如果 priority 相同，則擁有較高 IPv4 address 不會去搶著當 active
- 有兩個版本：都是 UDP port 1985 (被標註的是 HSRP group number)![](https://i.imgur.com/paL2I3j.png)
- Interface Tracking：如果被追蹤的介面掛掉，就自動扣 Priorty (預設 60)
- 狀態轉變![](https://i.imgur.com/U2Zv1aN.png)![](https://i.imgur.com/d0lk6tK.png)
#### Virtual Router Redundancy Protocol (VRRP) (RFC 2338![](https://i.imgur.com/1FVWwGT.png)
- 選舉方法同上，Active = Master，其他都是 Backup![](https://i.imgur.com/3Xs5vMH.png)
    - 被標註的是 Virtual Router IDentifier **VRID**
- 當把 priority 改得比較大時就會自動開啟 preemption
- 比較![](https://i.imgur.com/l54xAch.png)

### 網路協定 & Port Number
|簡稱|全名|Port|
|---|---|---|
|SMTP|Simple Mail Transfer Protocol|25|
|FTP|File Transfer Protocol|21|
|HTTP|Hypertext Transfer Protocol|80, 443|
|DNS|Domain Name System||
|SNMP|Simple Network Management Protocol|161, 162|
|SCTP|Stream Control Transmission Protocol||
|TCP|Transmission Control Protocol|6|
|UDP|User Datagram Protocol|17|
|ICMP|Internet Control Message Protocol|1|
|IGMP|Interne Group Management Protocol||
|IP|Internet Protocol||
|ARP|Address Resolution Protocol||
|RARP|Reversed Address Resolution Protocol||
