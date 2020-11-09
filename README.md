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

0x03. 非域渗透
----

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

    
