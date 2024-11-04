
## Basic

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#basic)

### City:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#city)

Find devices in a particular city.

```
city:"Bangalore"
```

### Country:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#country)

Find devices in a particular country.

```
country:"IN"
```

### Geo:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#geo)

Find devices by giving geographical coordinates.

```
geo:"56.913055,118.250862"
```

### Location

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#location)

```
country:us
country:ru
city:chicago
country:ru country:de city:chicago
```

### Hostname:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#hostname)

Find devices matching the hostname.

```
server: "gws" hostname:"google"
hostname:example.com
hostname:example.com,example.org
```

### Net:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#net)

Find devices based on an IP address or /x CIDR.

```
net:210.214.0.0/16
```

### Organization

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#organization)

```
org:microsoft
org:"United States Department"
```

### Autonomous System Number (ASN)

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#autonomous-system-number-asn)

```
asn:ASxxxx
```

### OS:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#os)

Find devices based on operating system.

```
os:"windows 7"
```

### Port:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#port)

Find devices based on open ports.

```
proftpd port:21
```

### Before/after:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#beforeafter)

Find devices before or after between a given time.

```
apache after:22/02/2009 before:14/3/2010
```

### SSL/TLS Certificates

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#ssltls-certificates)

- Self signed certificates

```
ssl.cert.issuer.cn:example.com ssl.cert.subject.cn:example.com
```

- Expired certificates

```
ssl.cert.expired:true
ssl.cert.subject.cn:example.com
```

### Device Type

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#device-type)

```
device:firewall
device:router
device:wap
device:webcam
device:media
device:"broadband router"
device:pbx
device:printer
device:switch
device:storage
device:specialized
device:phone
device:"voip phone"
device:"voip adaptor"
device:"load balancer"
device:"print server"
device:terminal
device:remote
device:telecom
device:power
device:proxy
device:pda
device:bridge
```

### Operating System

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#operating-system)

```
os:"windows 7"
os:"windows server 2012"
os:"linux 3.x"
```

### Product

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#product)

```
product:apache
product:nginx
product:android
product:chromecast
```

### Customer Premises Equipment (CPE)

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#customer-premises-equipment-cpe)

```
cpe:apple
cpe:microsoft
cpe:nginx
cpe:cisco
```

### Server

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#server)

```
server: nginx
server: apache
server: microsoft
server: cisco-ios
```

### ssh fingerprints

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#ssh-fingerprints)

```
dc:14:de:8e:d7:c1:15:43:23:82:25:81:d2:59:e8:c0
```

## Web

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#web)

### Pulse Secure

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#pulse-secure)

```
http.html:/dana-na
```

### PEM Certificates

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#pem-certificates)

```
http.title:"Index of /" http.html:".pem"
```

## Databases

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#databases)

### MySQL

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#mysql)

```
"product:MySQL"
```

### MongoDB

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#mongodb)

```
"product:MongoDB"
```

### elastic

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#elastic)

```
port:9200 json
```

### Memcached

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#memcached)

```
"product:Memcached"
```

### CouchDB

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#couchdb)

```
"product:CouchDB"
```

### PostgreSQL

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#postgresql)

```
"port:5432 PostgreSQL"
```

### Riak

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#riak)

```
"port:8087 Riak"
```

### Redis

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#redis)

```
"product:Redis"
```

### Cassandra

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#cassandra)

```
"product:Cassandra"
```

## Industrial Control Systems

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#industrial-control-systems)

### Samsung Electronic Billboards

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#samsung-electronic-billboards)

```
"Server: Prismview Player"
```

### Gas Station Pump Controllers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#gas-station-pump-controllers)

```
"in-tank inventory" port:10001
```

### Fuel Pumps connected to internet:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#fuel-pumps-connected-to-internet)

No auth required to access CLI terminal.

```
"privileged command" GET
```

### Automatic License Plate Readers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#automatic-license-plate-readers)

```
P372 "ANPR enabled"
```

### Traffic Light Controllers / Red Light Cameras

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#traffic-light-controllers--red-light-cameras)

```
mikrotik streetlight
```

### Voting Machines in the United States

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#voting-machines-in-the-united-states)

```
"voter system serial" country:US
```

### Open ATM:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#open-atm)

```
May allow for ATM Access availability
NCR Port:"161"
```

### Telcos Running Cisco Lawful Intercept Wiretaps

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#telcos-running-cisco-lawful-intercept-wiretaps)

```
"Cisco IOS" "ADVIPSERVICESK9_LI-M"
```

### Prison Pay Phones

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#prison-pay-phones)

```
"[2J[H Encartele Confidential"
```

### Tesla PowerPack Charging Status

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#tesla-powerpack-charging-status)

```
http.title:"Tesla PowerPack System" http.component:"d3" -ga3ca4f2
```

### Electric Vehicle Chargers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#electric-vehicle-chargers)

```
"Server: gSOAP/2.8" "Content-Length: 583"
```

### Maritime Satellites

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#maritime-satellites)

Shodan made a pretty sweet Ship Tracker that maps ship locations in real time, too!

```
"Cobham SATCOM" OR ("Sailor" "VSAT")
```

### Submarine Mission Control Dashboards

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#submarine-mission-control-dashboards)

```
title:"Slocum Fleet Mission Control"
```

### CAREL PlantVisor Refrigeration Units

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#carel-plantvisor-refrigeration-units)

```
"Server: CarelDataServer" "200 Document follows"
```

### Nordex Wind Turbine Farms

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#nordex-wind-turbine-farms)

```
http.title:"Nordex Control" "Windows 2000 5.0 x86" "Jetty/3.1 (JSP 1.1; Servlet 2.2; java 1.6.0_14)"
```

### C4 Max Commercial Vehicle GPS Trackers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#c4-max-commercial-vehicle-gps-trackers)

```
"[1m[35mWelcome on console"
```

### DICOM Medical X-Ray Machines

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#dicom-medical-x-ray-machines)

Secured by default, thankfully, but these 1,700+ machines still have no business being on the internet.

```
"DICOM Server Response" port:104
```

### GaugeTech Electricity Meters

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#gaugetech-electricity-meters)

```
"Server: EIG Embedded Web Server" "200 Document follows"
```

### Siemens Industrial Automation

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#siemens-industrial-automation)

```
"Siemens, SIMATIC" port:161
```

### Siemens HVAC Controllers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#siemens-hvac-controllers)

```
"Server: Microsoft-WinCE" "Content-Length: 12581"
```

### Door / Lock Access Controllers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#door--lock-access-controllers)

```
"HID VertX" port:4070
```

### Railroad Management

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#railroad-management)

```
"log off" "select the appropriate"
```

### Tesla Powerpack charging Status:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#tesla-powerpack-charging-status-1)

Helps to find the charging status of tesla powerpack.

```
http.title:"Tesla PowerPack System" http.component:"d3" -ga3ca4f2
```

### XZERES Wind Turbine

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#xzeres-wind-turbine)

```
title:"xzeres wind"
```

### PIPS Automated License Plate Reader

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#pips-automated-license-plate-reader)

```
"html:"PIPS Technology ALPR Processors""
```

### Modbus

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#modbus)

```
"port:502"
```

### Niagara Fox

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#niagara-fox)

```
"port:1911,4911 product:Niagara"
```

### GE-SRTP

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#ge-srtp)

```
"port:18245,18246 product:"general electric""
```

### MELSEC-Q

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#melsec-q)

```
"port:5006,5007 product:mitsubishi"
```

### CODESYS

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#codesys)

```
"port:2455 operating system"
```

### S7

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#s7)

```
"port:102"
```

### BACnet

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#bacnet)

```
"port:47808"
```

### HART-IP

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#hart-ip)

```
"port:5094 hart-ip"
```

### Omron FINS

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#omron-fins)

```
"port:9600 response code"
```

### IEC 60870-5-104

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#iec-60870-5-104)

```
"port:2404 asdu address"
```

### DNP3

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#dnp3)

```
"port:20000 source address"
```

### EtherNet/IP

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#ethernetip)

```
"port:44818"
```

### PCWorx

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#pcworx)

```
"port:1962 PLC"
```

### Crimson v3.0

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#crimson-v30)

```
"port:789 product:"Red Lion Controls"
```

### ProConOS

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#proconos)

```
"port:20547 PLC"
```

## Remote Desktop

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#remote-desktop)

### Unprotected VNC

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#unprotected-vnc)

```
"authentication disabled" port:5900,5901
"authentication disabled" "RFB 003.008"
```

### Windows RDP

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#windows-rdp)

99.99% are secured by a secondary Windows login screen.

```
"\x03\x00\x00\x0b\x06\xd0\x00\x00\x124\x00"
```

## Network Infrastructure

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#network-infrastructure)

### Hacked routers:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#hacked-routers)

Routers which got compromised

```
hacked-router-help-sos
```

### Redis open instances

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#redis-open-instances)

```
product:"Redis key-value store"
```

### Citrix:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#citrix)

Find Citrix Gateway.

```
title:"citrix gateway"
```

### Weave Scope Dashboards

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#weave-scope-dashboards)

Command-line access inside Kubernetes pods and Docker containers, and real-time visualization/monitoring of the entire infrastructure.

```
title:"Weave Scope" http.favicon.hash:567176827
```

### MongoDB

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#mongodb-1)

Older versions were insecure by default. Very scary.

```
"MongoDB Server Information" port:27017 -authentication
```

### Mongo Express Web GUI

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#mongo-express-web-gui)

Like the infamous phpMyAdmin but for MongoDB.

```
"Set-Cookie: mongo-express=" "200 OK"
```

### Jenkins CI

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#jenkins-ci)

```
"X-Jenkins" "Set-Cookie: JSESSIONID" http.title:"Dashboard"
```

### Jenkins:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#jenkins)

Jenkins Unrestricted Dashboard

```
x-jenkins 200
```

### Docker APIs

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#docker-apis)

```
"Docker Containers:" port:2375
```

### Docker Private Registries

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#docker-private-registries)

```
"Docker-Distribution-Api-Version: registry" "200 OK" -gitlab
```

### Pi-hole Open DNS Servers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#pi-hole-open-dns-servers)

```
"dnsmasq-pi-hole" "Recursion: enabled"
```

### Already Logged-In as root via Telnet

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#already-logged-in-as-root-via-telnet)

```
"root@" port:23 -login -password -name -Session
```

### Telnet Access:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#telnet-access)

NO password required for telnet access.

```
port:23 console gateway
```

### Polycom video-conference system no-auth shell

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#polycom-video-conference-system-no-auth-shell)

```
"polycom command shell"
```

### NPort serial-to-eth / MoCA devices without password

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#nport-serial-to-eth--moca-devices-without-password)

```
nport -keyin port:23
```

### Android Root Bridges

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#android-root-bridges)

A tangential result of Google's sloppy fractured update approach.

```
"Android Debug Bridge" "Device" port:5555
```

### Lantronix Serial-to-Ethernet Adapter Leaking Telnet Passwords

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#lantronix-serial-to-ethernet-adapter-leaking-telnet-passwords)

```
Lantronix password port:30718 -secured
```

### Citrix Virtual Apps

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#citrix-virtual-apps)

```
"Citrix Applications:" port:1604
```

### Cisco Smart Install

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#cisco-smart-install)

Vulnerable (kind of "by design," but especially when exposed).

```
"smart install client active"
```

### PBX IP Phone Gateways

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#pbx-ip-phone-gateways)

```
PBX "gateway console" -password port:23
```

### Polycom Video Conferencing

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#polycom-video-conferencing)

```
http.title:"- Polycom" "Server: lighttpd"
"Polycom Command Shell" -failed port:23
```

### Telnet Configuration:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#telnet-configuration)

```
"Polycom Command Shell" -failed port:23
```

### Bomgar Help Desk Portal

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#bomgar-help-desk-portal)

```
"Server: Bomgar" "200 OK"
```

### Intel Active Management CVE-2017-5689

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#intel-active-management-cve-2017-5689)

```
"Intel(R) Active Management Technology" port:623,664,16992,16993,16994,16995
"Active Management Technology"
```

### HP iLO 4 CVE-2017-12542

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#hp-ilo-4-cve-2017-12542)

```
HP-ILO-4 !"HP-ILO-4/2.53" !"HP-ILO-4/2.54" !"HP-ILO-4/2.55" !"HP-ILO-4/2.60" !"HP-ILO-4/2.61" !"HP-ILO-4/2.62" !"HP-iLO-4/2.70" port:1900
```

### Lantronix ethernet adapter’s admin interface without password

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#lantronix-ethernet-adapters-admin-interface-without-password)

```
"Press Enter for Setup Mode port:9999"
```

### Wifi Passwords:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#wifi-passwords)

Helps to find the cleartext wifi passwords in Shodan.

```
html:"def_wirelesspassword"
```

### Misconfigured Wordpress Sites:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#misconfigured-wordpress-sites)

The wp-config.php if accessed can give out the database credentials.

```
http.html:"* The wp-config.php creation script uses this file"
```

## Outlook Web Access:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#outlook-web-access)

### Exchange 2007

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#exchange-2007)

```
"x-owa-version" "IE=EmulateIE7" "Server: Microsoft-IIS/7.0"
```

### Exchange 2010

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#exchange-2010)

```
"x-owa-version" "IE=EmulateIE7" http.favicon.hash:442749392
```

### Exchange 2013 / 2016

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#exchange-2013--2016)

```
"X-AspNet-Version" http.title:"Outlook" -"x-owa-version"
```

### Lync / Skype for Business

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#lync--skype-for-business)

```
"X-MS-Server-Fqdn"
```

## Network Attached Storage (NAS)

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#network-attached-storage-nas)

### SMB (Samba) File Shares

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#smb-samba-file-shares)

Produces ~500,000 results...narrow down by adding "Documents" or "Videos", etc.

```
"Authentication: disabled" port:445
```

### Specifically domain controllers:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#specifically-domain-controllers)

```
"Authentication: disabled" NETLOGON SYSVOL -unix port:445
```

### Concerning default network shares of QuickBooks files:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#concerning-default-network-shares-of-quickbooks-files)

```
"Authentication: disabled" "Shared this folder to access QuickBooks files OverNetwork" -unix port:445
```

### FTP Servers with Anonymous Login

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#ftp-servers-with-anonymous-login)

```
"220" "230 Login successful." port:21
```

### Iomega / LenovoEMC NAS Drives

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#iomega--lenovoemc-nas-drives)

```
"Set-Cookie: iomega=" -"manage/login.html" -http.title:"Log In"
```

### Buffalo TeraStation NAS Drives

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#buffalo-terastation-nas-drives)

```
Redirecting sencha port:9000
```

### Logitech Media Servers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#logitech-media-servers)

```
"Server: Logitech Media Server" "200 OK"
```

### Plex Media Servers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#plex-media-servers)

```
"X-Plex-Protocol" "200 OK" port:32400
```

### Tautulli / PlexPy Dashboards

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#tautulli--plexpy-dashboards)

```
"CherryPy/5.1.0" "/home"
```

### Home router attached USB

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#home-router-attached-usb)

```
"IPC$ all storage devices"
```

## Webcams

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#webcams)

### D-Link webcams

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#d-link-webcams)

```
"d-Link Internet Camera, 200 OK"
```

### Hipcam

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#hipcam)

```
"Hipcam RealServer/V1.0"
```

### Yawcams

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#yawcams)

```
"Server: yawcam" "Mime-Type: text/html"
```

### webcamXP/webcam7

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#webcamxpwebcam7)

```
("webcam 7" OR "webcamXP") http.component:"mootools" -401
```

### Android IP Webcam Server

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#android-ip-webcam-server)

```
"Server: IP Webcam Server" "200 OK"
```

### Security DVRs

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#security-dvrs)

```
html:"DVR_H264 ActiveX"
```

### Surveillance Cams:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#surveillance-cams)

With username:admin and password: :P

```
NETSurveillance uc-httpd
Server: uc-httpd 1.0.0
```

## Printers & Copiers:

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#printers--copiers)

### HP Printers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#hp-printers)

```
"Serial Number:" "Built:" "Server: HP HTTP"
```

### Xerox Copiers/Printers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#xerox-copiersprinters)

```
ssl:"Xerox Generic Root"
```

### Epson Printers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#epson-printers)

```
"SERVER: EPSON_Linux UPnP" "200 OK"
"Server: EPSON-HTTP" "200 OK"
```

### Canon Printers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#canon-printers)

```
"Server: KS_HTTP" "200 OK"
"Server: CANON HTTP Server"
```

## Home Devices

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#home-devices)

### Yamaha Stereos

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#yamaha-stereos)

```
"Server: AV_Receiver" "HTTP/1.1 406"
```

### Apple AirPlay Receivers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#apple-airplay-receivers)

Apple TVs, HomePods, etc.

```
"\x08_airplay" port:5353
```

### Chromecasts / Smart TVs

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#chromecasts--smart-tvs)

```
"Chromecast:" port:8008
```

### Crestron Smart Home Controllers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#crestron-smart-home-controllers)

```
"Model: PYNG-HUB"
```

## Random Stuff

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#random-stuff)

### OctoPrint 3D Printer Controllers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#octoprint-3d-printer-controllers)

```
title:"OctoPrint" -title:"Login" http.favicon.hash:1307375944
```

### Etherium Miners

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#etherium-miners)

```
"ETH - Total speed"
```

### Apache Directory Listings

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#apache-directory-listings)

Substitute .pem with any extension or a filename like phpinfo.php.

```
http.title:"Index of /" http.html:".pem"
```

### Misconfigured WordPress

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#misconfigured-wordpress)

Exposed wp-config.php files containing database credentials.

```
http.html:"* The wp-config.php creation script uses this file"
```

### Too Many Minecraft Servers

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#too-many-minecraft-servers)

```
"Minecraft Server" "protocol 340" port:25565
```

### Literally Everything in North Korea

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Shodan%20Dorks.md#literally-everything-in-north-korea)

```
net:175.45.176.0/22,210.52.109.0/24,77.94.35.0/24
```


