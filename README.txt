"مشروع تخرج لنيل درجه اليكالريوس نخصص امن سيراني وشبكات "
Project: 'High availability and High security in Enterprice Infrastructure'
Author: Arslan alshamari <Arslan.Alshamari@gmail.com.com>

IP Address Ranges by Location 

================================================
Device Link 10.0.0.0/8 (Point-to-Point Links) /31
│
├── 10.10.0.0/16   DataCenter
├── 10.20.0.0/16   Branch 1
├── 10.30.0.0/16   Branch 2
-----------------------------------------------
Loopback 172.16.0.0/16	(uniq Ip ) /32
│
├── 172.16.10.0/24   DataCenter
├── 172.16.20.0/24   Branch 1
├── 172.16.30.0/24   Branch 2
-----------------------------------------------
Vlan 192.168.0.0/16	(255 host) /24
│
├── 192.168.10-19.0/24   DataCenter
├── 192.168.20-29.0/24   Branch 1
├── 192.168.30-39.0/24   Branch 2
#vlan 10-60 for all branch 
sit=Dc=1 ,vlan 10=192.168.11.0
sit=B1=2 ,vlan 20=192.168.22.0
sit=B2=3 ,vlan 30=192.168.33.0

sit=Dc=1 ,vlan 60=192.168.16.0
-----------------------------------------------
Frewall Addressing
192.168.0.0/16	(255 host) /24
│
├── 192.168.10.1-2 /30   DataCenter
├── 192.168.20.1-2 /30   Branch 1
├── 192.168.30.1-2 /30   Branch 2
-----------------------------------------------
Tunnel Addressing
│
├── 10.10.10.0/16   Tunnel 1 ISP 1
├── 10.10.20.0/16   Tunnel 2 ISP 2

----------------------------------------------
WAN 82.82.0.0/16 Loopback
│
├── 82.82.81.0/32   ISP 1
├── 82.82.82.0/32   ISP 2
----------------------
WAN 8.8.0.0/16 p2p link
│
├── 82.1.0.0/16   ISP 1
├── 82.2.2.0/16   ISP 2
================================================
Routing 
│
├── DataCenter
	├── ospf 1 area 1 for lan
	├── ospf 1 a 0 for mpls ISP 1
	├── ospf 1 a 0 for mpls ISP 2
├── Branch 1
	├── ospf 1 area 2 for lan
├── Branch 2
	├── eigrp 100 for lan
	├── ospf 1 area 3 for lan
	├── eigrp 100 for mpls ISP 1
	├── ospf 1 area 0 for mpls ISP 2
================================================
====================================
-قاعده عنونه loopback
172.16.<SITE>.<DEVICE sorting>
SITE-ID =10 ,Device=DC-RE1 == 172.16.10.1

-----------------------------------------------
-قاعده عنونه الربط بين الاجهزه
10.<SITE-ID>.<scours last number Loop0 IP +destination last number Loop0 IP>.<host> /31

SITE-ID 
-DC	10  ,-B1	20 ,-B2	30

امثله :
SITE-ID =10 ,scours Loop0 IP=R1(172.16.10.1):1 ,destination Loop0 IP=R2(172.16.10.2):2
==10.10.12.1/31 ,وفي الطرف الاحر 10.10.12.2/31
مثال اخر 
SITE-ID =20 ,scours Loop0 IP=B1-Core1(172.16.20.5):5 ,destination Loop0 IP=B1-DSw2(172.16.20.8):8
==10.20.58.1/31 ,وفي الطرف الاحر 10.20.58.2/31

وهكذا
-----------------------------------------------
قاعده عنونه ال vlan
VLAN 10,20,30,40,50
[192].[168].[SiteID/VLAN ID].[Host]
site :1 ,vlan 10 ==192.168.11.10
site :2 ,vlan 10 ==192.168.21.10
site :3 ,vlan 10 ==192.168.31.10
-----------------------------------------------
-قاعده عنونه الربط بين الاجهزه
10.<SITE-ID>.<255>.<host> /30
SITE-ID =10 ==10.10.255.10
======================================================



Hierarchical LAN Design Model
■ Access layer
■ Distribution layer
■ Core layer (