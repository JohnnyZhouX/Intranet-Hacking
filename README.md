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
2.msf/cs自带模块扫描
3.脚本扫描
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

        
0x02. 代理相关
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
    
VPN代理服务器
    常见vpn 协议：PPTP，L2TP，IPSec，SSLVPN，OpenVPN，搭建工具推荐：https://github.com/hwdsl2/setup-ipsec-vpn，https://github.com/SoftEtherVPN/SoftEtherVPN


```
     

0x03. 非域渗透
----
#### 1.
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

0x05. 常见工具介绍
----

0x06. 后门
----

0x07. 免杀相关
----

0x08. 案例分析
----

    
