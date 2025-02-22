# HangZhou Yushu Tech Unitree Go1
宇树科技 HangZhou Yushu Technology (Unitree) go1 development notes

* [HangZhou Yushu Tech Unitree Go1](#hangzhou-yushu-tech-unitree-go1)
* [Go1 series Product Matrix](#go1-series-product-matrix)
   * [Go1 (TM?)](#go1-tm)
   * [Go1 Air](#go1-air)
   * [Go1 Pro](#go1-pro)
   * [Go1 Pro MAX](#go1-pro-max)
   * [Go1 Nx](#go1-nx)
   * [Go1 MAX](#go1-max)
   * [Go1 Edu](#go1-edu)
   * [Go1 Edu Plus](#go1-edu-plus)
   * [Go1 Edu Explorer](#go1-edu-explorer)
* [Robot Internal Architecture](#robot-internal-architecture)
* [Expansion Header](#expansion-header)
* [Cameras - Super Sensory System](#cameras---super-sensory-system)
* [Programming interface](#programming-interface)
* [Update interface](#update-interface)
* [Upload interface](#upload-interface)
* [Passwords](#passwords)
* [Backup internal flash on all devices](#backup-internal-flash-on-all-devices)
* [Power Output](#power-output)
* [Installing TCPdump on the RasPi](#installing-tcpdump-on-the-raspi)
* [STM32 MicroROS?](#stm32-microros)
* [Bluetooth](#bluetooth)
* [Mobile App](#mobile-app)
* [45 / 5G support](#45--5g-support)
* [4G use in the USA](#4g-use-in-the-usa)
* [GPS from 4G module](#gps-from-4g-module)
* [Wifi backdoor](#wifi-backdoor)
* [Autostart items](#autostart-items)
* [PDB emergency shut off (backdoor? no way to disable)](#pdb-emergency-shut-off-backdoor-no-way-to-disable)
* [What talks to the STM at 192.168.123.10?](#what-talks-to-the-stm-at-19216812310)
* [MIT Cheetah code](#mit-cheetah-code)
* [Sniffing MQTT traffic on the dog](#sniffing-mqtt-traffic-on-the-dog)
* [Sending MQTT commands to the dog.](#sending-mqtt-commands-to-the-dog)
* [TFTP to RTOS](#tftp-to-rtos)
* [Troubleshooting](#troubleshooting)

This $2,700 robot dog will carry a single bottle of water for you: Who needs a tote bag when you have a little robot butler?<br>
https://www.theverge.com/2021/6/10/22527413/tiny-robot-dog-unitree-robotics-go1<br>
[![Launch Video](http://img.youtube.com/vi/xdfmhWQyp_8/0.jpg)](https://www.youtube.com/watch?v=xdfmhWQyp_8)<br>

# Go1 series Product Matrix
The full product matrix is not understood, there appear to be regional sub variants that are only sold in certain countries. For example the "Go1 MAX" is supposed to be China exclusive, although it can be easily obtained "cross-border". [Test report details](https://www.tele.soumu.go.jp/giteki/SearchServlet?pageID=jg01_01&PC=018&TC=N&PK=1&FN=220315N018&SN=%94F%8F%D8&LN=15&R1=*****&R2=*****) have given the current understanding of product options. <br>
<p align="center">
<img
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/JapanTest.png"><br>
<img
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/ChinaTest.png"><br>
</p>

## Go1 (TM?)
https://www.taobao.com/list/item/657740636451.htm
Early Black variant of the Air? 

https://www.cnbeta.com/articles/tech/1139381.htm
 
<p align="center">
<img 
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/Go1TM.jpg"><br>
</p>

<p align="center">
<img 
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/Go1.jpg"><br>
</p>

## Go1 Air
<p align="center">
<img 
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/Go1Air.png"><br>
</p>

## Go1 Pro
<p align="center">
<img 
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/Go1Pro.png"><br>
</p>

## Go1 Pro MAX
*unknown* 

## Go1 Nx
*unknown* 

## Go1 MAX
https://www.taobao.com/list/item/667863152779.htm
<p align="center">
<img 
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/Go1MAX.png"><br>
</p>

## Go1 Edu
<p align="center">
<img 
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/Go1EDU.png"><br>
</p>

When upgrading to the 2D or 3D LiDAR versions of the GO1 EDU, one of the three Jetson Nanos is upgraded to a Jetson Xavier NX. As a result, the robot is capable of dynamic obstacle avoidance, navigation planning, map building, self-positioning and more. This also supports your ability to develop gesture recognition, VSLAM, deep learning, machine learning, etc.

## Go1 Edu Plus
2D LiDAR Upgrade (Plus)

## Go1 Edu Explorer
3D LiDAR Upgrade (Explorer)

The difference between the EDU and the EDU Explorer is basically those features that comes with the integration of the Lidar (2D/3D): 
Basically<br>
- Obstacle avoidance<br>
- Mapping and navigation planning<br>
- Support for developing gesture recognition<br>
- VSLAM and other secondary development<br>
- With the 3D Lidar, also the Dynamic Obstacle Avoidance.<br>

# Robot Internal Architecture

<p align="center">
<img 
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/NetworkLayout.png"><br>
</p>

<p align="center">
<img 
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/FlowChart.png"><br>
</p>

<p align="center">
<img 
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/sdk.png"><br>
</p>

<p align="center">
<img 
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/arch.png"><br>
</p>

<p align="center">
<img 
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/Ports.png"><br>
</p>

Note: The two small pins next to the XT30U connector on the dog's belly appear to be P & N signals for the RS485 "motors" network on the "A4". <br>
XT30(2 2)-F<br>
https://www.aliexpress.com/item/3256801621419825.html

# Expansion Header
"40-pin Centronics connector"

<p align="center">
<img
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/AfterSalesSupport/Expansion/pinout.png"><br>
</p>

<p align="center">
<img
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/AfterSalesSupport/Expansion/Hirose40sFX2.png"><br>
</p>

PART: FX2CA2-40P-1.27DSAL(71)-ND<br>
DESC: CONN HEADER VERT 40POS 1.27MM<br>
MFG : Hirose Electric Co Ltd [CI] / FX2CA2-40P-1.27DSAL(71)<br>
https://www.hirose.com/product/document?clcode=CL0572-2768-1-71&productname=FX2-100P-0.635SH(71)&series=FX2&documenttype=Catalog&lang=en&documentid=D49368_en<br>
https://www.digikey.com/short/195n09w7<br>

# Cameras - Super Sensory System

Strings in the camera binary help us identify the vision hardware
```
unitree@unitree-desktop:~/Unitree/autostart/camerarosnode/cameraRosNode$ grep 2610 . -r
Binary file ./src/unitree_camera/lib/amd64/libtstc_V4L2_xu_camera.a matches
Binary file ./src/unitree_camera/lib/arm64/libtstc_V4L2_xu_camera.a matches
Binary file ./devel/lib/unitree_camera/point_cloud_node matches
Binary file ./devel/lib/unitree_camera/example_point matches
```

SPCA_2610 must be the camera name. 

```
source//Extension_Unit_Class/Extension_Unit_SPCA2650_Protocol.cpp
```

This is clearly a SunPlus based "SSS" system. 
https://www.synopsys.com/dw/doc.php/ss/SunPlusIT_usb3.0-phy-controller.pdf
https://www.sunplusit.com/EN/Product/PcCamera

Each Jetson Nano includes the following USB devices, in some cases multiple per.
```
Bus 001 Device 002: ID 1bcf:2cd1 Sunplus Innovation Technology Inc. 
```

The linux hardware database lists the camera package here:
https://linux-hardware.org/index.php?id=usb:1bcf-2cd1
"Sunplus Innovation Technology USB2.0 Camera"


# Programming interface
In Go1_2022_05_11_e0d0e617/raspi/Unitree/autostart/programming we find programming.py<br>
It imports ./build/robot_interface_high_level.cpython-37m-aarch64-linux-gnu.so in order to call the UDP listen functions. 
```
import robot_interface_high_level as robot_interface
``` 
...
```
unitree_go1 = robot_interface.RobotInterface()
```

The interface seems to blindly pass user input to exec().
```
The exec() method executes the dynamically created program, which is either a string or a code object.
```

First the code passes through compile()
```
compile() method is used if the Python code is in string form or is an AST object, and you want to change it to a code object.
```
This handles all the MIT Scratch code blocks from the mobile client. 

# Update interface
In Go1_2021_12_10_d799e0c3/raspi/Unitree/autostart/updateDependencies we find startup_manager.py<br>
It declares itself to be "Unitree System Manager", and offers the following functions
```
Functions:
1. run bash files
2. delete uploaded packages
3. run update packages
4. process topics when modules shut down
```

This can also be used to run arbitry commands. 
```
def on_message(client, userdata, msg):
    global updatePackage
    global updateFirmware
    # not doing anything during update
    if(updatePackage !='' or updateFirmware !=''):
        return 
    # run bash file
    if(msg.topic == "usys/sh"):
        bashFile = str(msg.payload,'utf-8')
        print("Running sh " + bashFile)
        process = subprocess.Popen(["sh", bashFile],stdout=subprocess.PIPE)
```

# Upload interface 
In Go1_2021_12_10_d799e0c3/raspi/Unitree/autostart/updateDependencies we find startup_uploader.py<br>
It outlines how to accept update packages. They must be .zip files, or they will be rejected

```
$ cat test.txt 
------------------------------4ebf00fbcf09
Content-Disposition: form-data; name="file"; filename="/tmp/out.zip"

filecontent here

------------------------------4ebf00fbcf09

$ curl -X POST -H "Content-Type: multipart/form-data; boundary=----------------------------4ebf00fbcf09"   --data-binary @test.txt http://localhost:9800
{'info':'File '/tmp/out.zip' upload success!'}
```

# Passwords

raspberrypi<br>
192.168.123.161<br>
192.168.12.1<br>
pi / 123<br>
root / 123<br>

nano2gb<br>
192.168.123.13<br>
unitree / 123<br>
root / (disabled)

unitree-desktop<br>
192.168.123.14<br>
192.168.123.15<br>
unitree / 123<br>
root / (disabled)

# Backup internal flash on all devices

Ssh into the raspi, dump it to external USB
```
root@raspberrypi:/media/pi/59f46a9c-a6fc-45d6-824e-55f5c3844716/go1/raspberrypi# dd if=/dev/mmcblk0 of=mmcblk0 bs=4096
^C521+0 records in
521+0 records out
2134016 bytes (2.1 MB, 2.0 MiB) copied, 0.0781444 s, 27.3 MB/s
```

Ssh to each of the "desktop" nanos and dump them
```
root@unitree-desktop:/home/unitree# dd if=/dev/mmcblk0 bs=4096 | gzip -c | ssh pi@192.168.123.161 'cat > /media/pi/59f46a9c-a6fc-45d6-824e-55f5c3844716/go1/ubuntu-desktop_1/mmcblk0.gz'
pi@192.168.123.161's password: 
root@unitree-desktop:/home/unitree# dd if=/dev/mmcblk0 bs=4096 | gzip -c | ssh pi@192.168.123.161 'cat > /media/pi/59f46a9c-a6fc-45d6-824e-55f5c3844716/go1/ubuntu-desktop_2/mmcblk0.gz'
pi@192.168.123.161's password: 
```

Ssh to the nano2gb and dump it 
```
root@nano2gb:/home/unitree# dd if=/dev/mmcblk0 bs=4096 | gzip -c | ssh pi@192.168.123.161 'cat > /media/pi/59f46a9c-a6fc-45d6-824e-55f5c3844716/go1/nano2gb/mmcblk0.gz'
pi@192.168.123.161's password: 
```

# Power Output 
On the dogs belly is a 24v pass though assumed to be 2A max.

# Installing TCPdump on the RasPi

Download from the mirror
```
$ wget https://mirrors.tuna.tsinghua.edu.cn/debian/pool/main/t/tcpdump/tcpdump_4.9.3-1~deb10u2_arm64.deb 
--2022-07-06 15:30:55--  https://mirrors.tuna.tsinghua.edu.cn/debian/pool/main/t/tcpdump/tcpdump_4.9.3-1~deb10u2_arm64.deb
Resolving mirrors.tuna.tsinghua.edu.cn (mirrors.tuna.tsinghua.edu.cn)... 101.6.15.130, 2402:f000:1:400::2
Connecting to mirrors.tuna.tsinghua.edu.cn (mirrors.tuna.tsinghua.edu.cn)|101.6.15.130|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 378080 (369K) [application/octet-stream]
Saving to: ‘tcpdump_4.9.3-1~deb10u2_arm64.deb’

tcpdump_4.9.3-1~deb 100%[===================>] 369.22K   290KB/s    in 1.3s    

2022-07-06 15:31:00 (290 KB/s) - ‘tcpdump_4.9.3-1~deb10u2_arm64.deb’ saved [378080/378080]
```

Scp to the raspi, and install. 

```
$ scp tcpdump_4.9.3-1~deb10u2_arm64.deb pi@192.168.123.161:/tmp/
pi@192.168.123.161's password: 
tcpdump_4.9.3-1~deb10u2_arm64.deb                                                    100%  369KB   
```

Make yourself root and install the package. 
```
root@raspberrypi:/home/pi$ dpkg -i /tmp/tcpdump_4.9.3-1~deb10u2_arm64.deb 
Selecting previously unselected package tcpdump.
(Reading database ... 171570 files and directories currently installed.)
Preparing to unpack .../tcpdump_4.9.3-1~deb10u2_arm64.deb ...
Unpacking tcpdump (4.9.3-1~deb10u2) ...
Setting up tcpdump (4.9.3-1~deb10u2) ...
Processing triggers for man-db (2.8.5-2) ...
```

# STM32 MicroROS?

The device at 192.168.123.10 may be an STM32 running MicroROS

https://micro.ros.org/docs/overview/hardware/<br>
https://www.youtube.com/watch?v=Sz-nllmtcc8<br>
https://github.com/micro-ROS/micro_ros_stm32cubemx_utils<br>

Interface port documentation reveals it to be an "H7", and an "A4"<br>
STM32H7 - https://www.st.com/en/microcontrollers-microprocessors/stm32h7-series.html<br>
https://github.com/micro-ROS/NuttX/blob/master/arch/arm/src/stm32h7/stm32_gpio.h
# Bluetooth 

The transmitter appears to be Bluetooth based. 

# Mobile App
The mobile app uses MQTT over websocket

On an iOS device you can use RVI utils to sniff the connection
https://developer.apple.com/documentation/network/recording_a_packet_trace

$ rvictl -s 0000xxxx-yourdeviceuuid

Starting device 0000xxxx-yourdeviceuuid [SUCCEEDED] with interface rvi0

$ sudo tcpdump -i rvi0 -xX -s2000 host 192.168.12.1 and not port domain -w tcpdump.pcap

The initial connection hits /mqtt on the web server. 

```
GET /mqtt HTTP/1.1
Host: 192.168.12.1
Pragma: no-cache
Accept: */*
Sec-WebSocket-Key: qoldXnNLZu0GftYE7x+XgA==
Sec-WebSocket-Version: 13
Sec-WebSocket-Extensions: permessage-deflate
Sec-WebSocket-Protocol: mqtt
Cache-Control: no-cache
Accept-Language: en-US,en;q=0.9
Origin: capacitor://localhost
User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 15_5 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148
Connection: Upgrade
Accept-Encoding: gzip, deflate
Upgrade: websocket
```

It immediately switches to Websocket protocol. 

```
HTTP/1.1 101 Switching Protocols
Server: nginx/1.14.2
Date: Sat, 06 Nov 2021 02:17:43 GMT
Connection: upgrade
Upgrade: WebSocket
Sec-WebSocket-Accept: aLEJi/WW+zQ1NjZiE5SszGyjI+4=
Sec-WebSocket-Protocol: mqtt

```

You can take apart the supporting .js files and make them more readable 
with "prettier". They are Webpack 4 encoded files. 

```
$ node bin-prettier.js ../../chunk-ab73ca30.b65f7572.js
```

You can find the respective files in:<br>
Go1_2021_12_10_d799e0c3/raspi/Unitree/autostart/webMonitor/dist/

The MQTT locic can be further understood by disassembling appTransit. 

```
  bVar1 = std::operator==(pbVar3,"controller/action");
  if (bVar1 != false) {
    pmVar2 = (message *)
             std::__shared_ptr_access<mqtt::message_const,(__gnu_cxx::_Lock_policy)2,false,false>::
             operator->(this_01);
    pbVar3 = (basic_string *)mqtt::message::get_payload_str[abi:cxx11](pmVar2);
    pbVar4 = std::operator<<((basic_ostream *)&std::cout,pbVar3);
    std::basic_ostream<char,std::char_traits<char>>::operator<<
              ((basic_ostream<char,std::char_traits<char>> *)pbVar4,
               std::endl<char,std::char_traits<char>>);
    pmVar2 = (message *)
             std::__shared_ptr_access<mqtt::message_const,(__gnu_cxx::_Lock_policy)2,false,false>::
             operator->(this_01);
    mqtt::message::get_payload_str[abi:cxx11](pmVar2);
    std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>::basic_string
              (abStack48);
                    /* try { // try from 0010bf9c to 0010bfe3 has its CatchHandler @ 0010c458 */
    std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>::operator=
              ((basic_string<char,std::char_traits<char>,std::allocator<char>> *)(this + 0x970),
               abStack48);
    bVar1 = std::operator==(abStack48,"walk");
    if (bVar1 == false) {
      bVar1 = std::operator==(abStack48,"run");
      if (bVar1 == false) {
        bVar1 = std::operator==(abStack48,"climb");
        if (bVar1 == false) {
          bVar1 = std::operator==(abStack48,"stand");
          if (bVar1 == false) {
            bVar1 = std::operator==(abStack48,"dance1");
            if (bVar1 == false) {
              bVar1 = std::operator==(abStack48,"dance2");
              if (bVar1 == false) {
                bVar1 = std::operator==(abStack48,"dance3");
                if (bVar1 == false) {
                  bVar1 = std::operator==(abStack48,"dance4");
                  if (bVar1 == false) {
                    bVar1 = std::operator==(abStack48,"backflip");
                    if (bVar1 == false) {
                      bVar1 = std::operator==(abStack48,"jumpYaw");
                      if (bVar1 == false) {
                        bVar1 = std::operator==(abStack48,"straightHand1");
                        if (bVar1 == false) {
                          bVar1 = std::operator==(abStack48,"standUp");
                          if (bVar1 == false) {
                            bVar1 = std::operator==(abStack48,"standDown");
                            if (bVar1 == false) {
                              bVar1 = std::operator==(abStack48,"damping");
                              if (bVar1 == false) {
                                bVar1 = std::operator==(abStack48,"recoverStand");
                                if (bVar1 != false) {
```


# 45 / 5G support

Quectel EG25-G is connected to the RasPI
https://www.quectel.com/wp-content/uploads/pdfupload/EP-FMEG25GMPCIs_Specification_V1.0-1609137.pdf
https://www.t-mobile.com/content/dam/tfb/pdf/tfb-iot/Quectel_EG25-G_LTE_Standard_Specification_V1.3.pdf
https://fccid.io/XMR201903EG25G/User-Manual/user-manual-4219711.pdf

It includes a GNSS function. The GPS antenna in the Go1 is connected to this device. 

5G support is assumed to be provided by a Quctel RM5 series chipset. 
https://www.quectel.com/product/5g-rm50xq-series
https://www.quectel.com/product/5g-rm510q-gl
https://www.quectel.com/wp-content/uploads/2021/02/Quectel_Product_Brochure_EN_V6.1.pdf

CVE-2021-31698: Quectel EG25-G devices through 202006130814 allow executing arbitrary code remotely by using an AT command to place shell metacharacters in quectel_handle_fumo_cfg input in atfwd_daemon.<br>
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-31698
"Code execution as root via AT commands on the Quectel EG25-G modem"
https://nns.ee/blog/2021/04/03/modem-rce.html

While connected to the 45/5g the dog does call home. Here is an example of it calling the Zhexi cloud

```
pi@raspberrypi:~ $ netstat -ap | grep ESTABLISHED | grep 100.100.57.114
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
tcp        0      0 100.100.57.114:53570    124.156.140.55:5670     ESTABLISHED -                   
tcp        0      0 100.100.57.114:52582    124.156.140.55:http     ESTABLISHED -                   
tcp        0      0 100.100.57.114:52578    124.156.140.55:http     ESTABLISHED -                   
tcp        0      0 100.100.57.114:55788    134.175.175.55:9998     ESTABLISHED -                   
```

<p align="center">
<img
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/zhexi.png"><br>
<img
src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/dns.png"><br>
</p>

You can disbale the tunnel by killing the cloudsail daemon
```
root@raspberrypi:/home/pi/Unitree/autostart# systemctl disable CSClientDaemon
Removed /etc/systemd/system/multi-user.target.wants/CSClientDaemon.service.
```

Also move the auto start "tunnel" out of the way so it is unable to autostart
```
root@raspberrypi:/home/pi/Unitree/autostart# mv tunnel/ /root/tunnel_disabled/

```

# 4G use in the USA

Support provided by Quectel EC25<br>
https://osmocom.org/projects/quectel-modems/wiki/EC25_Linux<br>
Known to be ridden with FOTA backdoors<br>
https://penthertz.com/blog/mobile-iot-modules-FOTA-backdooring-at-scale.html<br>
"All the 4G Modules Could be Hacked" talk from Defcon 2019<br>
https://i.blackhat.com/USA-19/Wednesday/us-19-Shupeng-All-The-4G-Modules-Could-Be-Hacked.pdf
https://nns.ee/blog/2021/04/03/modem-rce.html

The variant tested was not vulnerable to the obvious code execution: https://nvd.nist.gov/vuln/detail/CVE-2021-31698

```
root@raspberrypi:~# lsusb | grep Quec
Bus 001 Device 003: ID 2c7c:0125 Quectel Wireless Solutions Co., Ltd. EC25 LTE modem

root@raspberrypi:~#  minicom -b 115200 -D /dev/ttyUSB2 


Welcome to minicom 2.7.1

OPTIONS: I18n 
Compiled on May  6 2018, 07:48:54.
Port /dev/ttyUSB2, 18:07:01

Press CTRL-A Z for help on special keys                                                                                                                                                                                          
                                                                                                                                                                                                                                 
ATE1<enter>                                                                                                                                                                                                                                 
OK                       

ATI
Quectel
EC20F
Revision: EC20CEFRSGR08A03M2G

AT+QFUMOCFG=?
+QFUMOCFG: "update",(0,1)

OK
AT+QFUMOCFG="dmacc","`reboot`"
ERROR
```

Additionally ADB is disabled in firmware per: https://forums.quectel.com/t/eg25-g-cannot-enable-adb-with-at-command/4809
"ADB port in disblae in firmware. It’s not able to be used in standard module."

By default the enable command is refused. 
```
AT+QCFG="usbcfg",0x2c7c,0x125,1,1,1,1,1,1,1
OK                                                                                                                 
AT+QCFG="usbcfg"                                                                                                   
+QCFG: "usbcfg",0x2C7C,0x0125,1,1,1,1,1,0,1                                                                        
                                                                                                                   
OK 
```

You can use an unlocker tool however after using the AT command to obtain the key 
https://xnux.eu/devices/feature/qadbkey-unlock.c

```
AT+QADBKEY?
+QADBKEY: 39804286
```

```
root@raspberrypi:~# wget https://xnux.eu/devices/feature/qadbkey-unlock.c
--2022-07-13 18:59:07--  https://xnux.eu/devices/feature/qadbkey-unlock.c
Resolving xnux.eu (xnux.eu)... 195.181.215.36, 2001:15e8:110:3624::1
Connecting to xnux.eu (xnux.eu)|195.181.215.36|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 658 [text/plain]
Saving to: ‘qadbkey-unlock.c’

qadbkey-unlock.c                                  100%[=============================================================================================================>]     658  
--.-KB/s    in 0s      

2022-07-13 18:59:09 (1.41 MB/s) - ‘qadbkey-unlock.c’ saved [658/658]

root@raspberrypi:~# gcc qadbkey-unlock.c -o qadbkey-unlock -lcrypt
root@raspberrypi:~# ./qadbkey-unlock 
Usage: unlock <serial>
Use AT+QADBKEY? to get the serial number.
root@raspberrypi:~# ./qadbkey-unlock 39804286
AT+QADBKEY="OyFBlcSkpqh9Xt2i"
AT+QCFG="usbcfg",0x2C7C,0x125,1,1,1,1,1,1,0

To disable ADB, run: (beware that modem will not be able to enter sleep with ADB enabled!!)
AT+QCFG="usbcfg",0x2C7C,0x125,1,1,1,1,1,0,0

pi@raspberrypi:~ $ adb devices
List of devices attached
* daemon not running; starting now at tcp:5037
* daemon started successfully
(no serial number)	device

pi@raspberrypi:~ $ adb shell
/ # hostname
mdm9607
/ # id
uid=0(root) gid=0(root) groups=1004,1007,1011,1015(sdcard),1028,3001,3002,3003,3006
```

If you see this, you may need to reboot. 
```
root@raspberrypi:/home/pi# adb devices
List of devices attached
(no serial number)	no permissions (user in plugdev group; are your udev rules wrong?); see [http://developer.android.com/tools/device.html]
```

Alternately you can try:
```
root@raspberrypi:/home/pi# sudo usermod -aG plugdev $LOGNAME
root@raspberrypi:/etc/udev/rules.d# cat > 51-android.rules
SUBSYSTEM=="usb",ATTRS{idVendor}=="2c7c",ATTRS{idProduct}=="0125",MODE="0666",GROUP="plugdev"
root@raspberrypi:/etc/udev/rules.d# udevadm control --reload-rules
```
and reboot

Get a T-Mobile SIM card. 

Edit the config file for the Unitree configNetwork autostart service, at the very least the APN needs to be changed off China Unicom.
```
pi@raspberrypi:~ $ diff bk_Unitree/ Unitree -ru
diff -ru bk_Unitree/autostart/configNetwork/ppp/quectel-chat-connect Unitree/autostart/configNetwork/ppp/quectel-chat-connect
--- bk_Unitree/autostart/configNetwork/ppp/quectel-chat-connect	2021-11-05 04:31:12.986184175 -0900
+++ Unitree/autostart/configNetwork/ppp/quectel-chat-connect	2021-11-05 18:29:08.267718437 -0900
@@ -9,6 +9,6 @@
 OK ATE0
 OK ATI;+CSUB;+CSQ;+CPIN?;+COPS?;+CGREG?;&D2
 # Insert the APN provided by your network operator, default apn is 3gnet
-OK AT+CGDCONT=1,"IP","3gnet",,0,0
+OK AT+CGDCONT=1,"IP","fast.t-mobile.com",,0,0
 OK ATD*99#
 CONNECT
diff -ru bk_Unitree/autostart/configNetwork/ppp/quectel-ppp Unitree/autostart/configNetwork/ppp/quectel-ppp
--- bk_Unitree/autostart/configNetwork/ppp/quectel-ppp	2021-11-05 04:31:12.986184175 -0900
+++ Unitree/autostart/configNetwork/ppp/quectel-ppp	2022-07-08 07:20:32.160480515 -0900
@@ -3,7 +3,7 @@
 #Modem path, like /dev/ttyUSB3,/dev/ttyACM0, depend on your module, default path is /dev/ttyUSB3
 /dev/ttyUSB3 115200
 #Insert the username and password for authentication, default user and password are test
-user "test" password "test"
+user "user" password "password"
 # The chat script, customize your APN in this file
 connect 'chat -s -v -f /etc/ppp/peers/quectel-chat-connect'
 # The close script
diff -ru bk_Unitree/autostart/configNetwork/ppp/quectel-pppd.sh Unitree/autostart/configNetwork/ppp/quectel-pppd.sh
--- bk_Unitree/autostart/configNetwork/ppp/quectel-pppd.sh	2021-11-05 04:31:12.986184175 -0900
+++ Unitree/autostart/configNetwork/ppp/quectel-pppd.sh	2022-07-08 07:20:48.641378405 -0900
@@ -3,9 +3,9 @@
 #quectel-pppd devname apn user password
 echo "quectel-pppd options in effect:"
 QL_DEVNAME=/dev/ttyUSB3
-QL_APN=3gnet
-QL_USER=user
-QL_PASSWORD=passwd
+QL_APN=fast.t-mobile.com
+QL_USER="user"
+QL_PASSWORD="password"
 if [ $# -ge 1 ]; then
 	QL_DEVNAME=$1	
 	echo "devname   $QL_DEVNAME    # (from command line)"

```

You'll need to add the libqmi tools. 

```
root@raspberrypi:/home/pi$ apt-get update
root@raspberrypi:/home/pi$ apt-get install libqmi-utils
```

The mmcli tool will help get basic informaiton that you may need to give your cellular provider such as IMEI, and ESN. You can also make sure the device is not SIM locked. 

```

root@raspberrypi:/home/pi$ mmcli -m 0
  --------------------------------
  General  |            dbus path: /org/freedesktop/ModemManager1/Modem/0
           |            device id: 
  --------------------------------
  Hardware |         manufacturer: QUALCOMM INCORPORATED
           |                model: QUECTEL Mobile Broadband Module
           |             revision: 
           |         h/w revision: 10000
           |            supported: gsm-umts, lte
           |                       cdma-evdo, lte
           |                       lte
           |                       cdma-evdo, gsm-umts, lte
           |              current: cdma-evdo, gsm-umts, lte
           |         equipment id: 
  --------------------------------
  System   |               device: /sys/devices/platform/soc/fe980000.usb/usb1/1-1/1-1.3
           |              drivers: option1, qmi_wwan
           |               plugin: Quectel
           |         primary port: cdc-wdm0
           |                ports: ttyUSB0 (qcdm), ttyUSB2 (at), cdc-wdm0 (qmi), wwan0 (net), 
           |                       ttyUSB3 (at)
  --------------------------------
  Status   |                 lock: sim-pin2
           |       unlock retries: sim-pin (3), sim-pin2 (10), sim-puk (10), sim-puk2 (10)
           |                state: disabled
           |          power state: on
           |       signal quality: 0% (cached)
  --------------------------------
  Modes    |            supported: allowed: 2g; preferred: none
           |                       allowed: 3g; preferred: none
           |                       allowed: 2g, 3g; preferred: 3g
           |                       allowed: 2g, 3g; preferred: 2g
           |                       allowed: 2g, 4g; preferred: 4g
           |                       allowed: 2g, 4g; preferred: 2g
           |                       allowed: 3g, 4g; preferred: 3g
           |                       allowed: 3g, 4g; preferred: 4g
           |                       allowed: 2g, 3g, 4g; preferred: 4g
           |                       allowed: 2g, 3g, 4g; preferred: 3g
           |                       allowed: 2g, 3g, 4g; preferred: 2g
           |              current: allowed: 2g, 3g, 4g; preferred: 4g
  --------------------------------
  Bands    |            supported: egsm, dcs, utran-1, utran-8, eutran-1, eutran-3, eutran-5, 
           |                       eutran-8, eutran-34, eutran-38, eutran-39, eutran-40, eutran-41, 
           |                       cdma-bc0
           |              current: egsm, dcs, utran-1, utran-8, eutran-1, eutran-3, eutran-5, 
           |                       eutran-8, eutran-34, eutran-38, eutran-39, eutran-40, eutran-41, 
           |                       cdma-bc0
  --------------------------------
  IP       |            supported: ipv4, ipv6, ipv4v6
  --------------------------------
  3GPP     |                 imei: 313376969187
  --------------------------------
  3GPP EPS | ue mode of operation: csps-2
  --------------------------------
  CDMA     |                 meid: DEADBEEFCAFEBABE
           |                  esn: BEEFCAFE
           |           activation: not-activated
  --------------------------------
  SIM      |            dbus path: /org/freedesktop/ModemManager1/SIM/0
```

If you need to double check the bearer information you can. 

```
root@raspberrypi:/home/pi$ mmcli -b 0
  --------------------------------
  General            |  dbus path: /org/freedesktop/ModemManager1/Bearer/0
                     |       type: default
  --------------------------------
  Status             |  connected: yes
                     |  suspended: no
                     |  interface: wwan0
                     | ip timeout: 20
  --------------------------------
  Properties         |        apn: fast.t-mobile.com
                     |    roaming: allowed
  --------------------------------
  IPv4 configuration |     method: static
                     |    address: 5.4.3.1
                     |     prefix: 30
                     |    gateway: 5.4.3.2
                     |        dns: 1.1.0.4, 1.1.0.2
                     |        mtu: 1500
  --------------------------------
  Statistics         |   duration: 330
```

You can use qmicli to verify the APN profile setting slots

```
root@raspberrypi:/home/pi$ qmicli -p -d /dev/cdc-wdm0 --wds-get-profile-list=3gpp
Profile list retrieved:
	[1] 3gpp - 
		APN: 'fast.t-mobile.com'
		PDP type: 'ipv4'
		PDP context number: '1'
		Username: ''
		Password: ''
		Auth: 'none'
		No roaming: 'no'
		APN disabled: 'no'
	[2] 3gpp - 
		APN: 'ims'
		PDP type: 'ipv4-or-ipv6'
		PDP context number: '2'
		Username: ''
		Password: ''
		Auth: 'none'
		No roaming: 'no'
		APN disabled: 'no'
	[3] 3gpp - 
		APN: ''
		PDP type: 'ipv4-or-ipv6'
		PDP context number: '3'
		Username: ''
		Password: ''
		Auth: 'none'
		No roaming: 'no'
		APN disabled: 'no'

``` 

Scanning for available networks is a good way to troubleshoot as well 

```
root@raspberrypi:/home/pi$ mmcli -m 0 --3gpp-scan --timeout=300
  ---------------------
  3GPP scan | networks: 312250 - T-Mobile (lte, current)
            |           311490 - 311 490 (lte, available)
            |           311882 - 311 882 (lte, available)
            |           312530 - 312 530 (lte, available)
            |           310120 - Sprint (lte, available)

```

# GPS from 4G module

```
root@raspberrypi:/home/pi$ mmcli -m 0 --location-status
  ------------------------
  Location | capabilities: 3gpp-lac-ci, gps-raw, gps-nmea, cdma-bs, agps
           |      enabled: 3gpp-lac-ci, cdma-bs
           |      signals: no
  ------------------------
  GPS      | refresh rate: 30 seconds
root@raspberrypi:/home/pi$ mmcli -m 0 --location-enable-gps-raw --location-enable-gps-nmea
successfully setup location gathering
root@raspberrypi:/home/pi$ mmcli -m 0 --location-get
  --------------------------
  3GPP |      operator code: XX
       |      operator name: YY
       | location area code: ZZ
       | tracking area code: AA
       |            cell id: 0000000000
  --------------------------
  GPS  |               nmea: $GPGGA,,,,,,0,,,,,,,,*66
       |                     $GPGSA,A,1,,,,,,,,,,,,,,,,*32
       |                     $GPVTG,,T,,M,,N,,K,N*2C
       |                     $GPRMC,,V,,,,,,,,,,N*53
       |                     $GPGSV,1,1,02,00,,,00,00,,,00,1*68 

```

# Wifi backdoor
There is an autoconnect network called "Unitree-2.4G" in the wpa supplicant config. 

```

pi@raspberrypi:/etc $ cat ./wpa_supplicant/wpa_supplicant.conf
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US
 
network={
	ssid="Unitree-5G"
	psk="Unitree#9035"
	key_mgmt=WPA-PSK
	disabled=1
}
 
network={
	ssid="Unitree-WiFi-5G"
	psk="Unitree#9035"
	key_mgmt=WPA-PSK
	disabled=1
}
 
network={
	ssid="Unitree-2.4G"
	psk="Unitree#9035"
	key_mgmt=WPA-PSK
}
```

Supplicant auto starts at boot

```
pi@raspberrypi:/etc $ ps -ax | grep wpa
  470 ?        Ss     0:00 /sbin/wpa_supplicant -u -s -O /run/wpa_supplicant
  756 ?        Ss     0:00 wpa_supplicant -B -c/etc/wpa_supplicant/wpa_supplicant.conf -iwlan0 -Dnl80211,wext
 8444 pts/1    S+     0:00 grep --color=auto wpa
```

If you are quick you can catch it to login to the dog. 

```
$ ping 192.168.1.115
PING 192.168.1.115 (192.168.1.115): 56 data bytes
Request timeout for icmp_seq 0
Request timeout for icmp_seq 1
Request timeout for icmp_seq 2
Request timeout for icmp_seq 3
Request timeout for icmp_seq 4
Request timeout for icmp_seq 5
Request timeout for icmp_seq 6
ping: sendto: No route to host
Request timeout for icmp_seq 7
ping: sendto: Host is down
Request timeout for icmp_seq 8
ping: sendto: Host is down
Request timeout for icmp_seq 9
ping: sendto: Host is down
Request timeout for icmp_seq 10
ping: sendto: Host is down
Request timeout for icmp_seq 11
ping: sendto: Host is down
Request timeout for icmp_seq 12
Request timeout for icmp_seq 13
64 bytes from 192.168.1.115: icmp_seq=14 ttl=64 time=5.955 ms
64 bytes from 192.168.1.115: icmp_seq=15 ttl=64 time=2.563 ms
64 bytes from 192.168.1.115: icmp_seq=16 ttl=64 time=3.939 ms
64 bytes from 192.168.1.115: icmp_seq=17 ttl=64 time=3.791 ms
64 bytes from 192.168.1.115: icmp_seq=18 ttl=64 time=3.299 ms
Request timeout for icmp_seq 19
Request timeout for icmp_seq 20
Request timeout for icmp_seq 21
Request timeout for icmp_seq 22
Request timeout for icmp_seq 23
Request timeout for icmp_seq 24

Roughly 40 seconds into the boot process this is available for literally 5 seconds. 

```

Default credentials work as expected 


```

$ ssh -o StrictHostKeyChecking=accept-new -v pi@192.168.1.115 "hostname;id;exit"
OpenSSH_8.6p1, LibreSSL 3.3.6
...
debug1: Connecting to 192.168.1.115 [192.168.1.115] port 22.
debug1: Connection established.
...
debug1: Local version string SSH-2.0-OpenSSH_8.6
debug1: Remote protocol version 2.0, remote software version OpenSSH_7.9p1 Debian-10+deb10u2+rpt1
debug1: compat_banner: match: OpenSSH_7.9p1 Debian-10+deb10u2+rpt1 pat OpenSSH* compat 0x04000000
debug1: Authenticating to 192.168.1.115:22 as 'pi'
...
debug1: Next authentication method: password
pi@192.168.1.115's password: 
debug1: Authentication succeeded (password).
Authenticated to 192.168.1.115 ([192.168.1.115]:22).
...
debug1: Sending command: hostname;id;exit
...
raspberrypi
uid=1000(pi) gid=1000(pi) groups=1000(pi),4(adm),20(dialout),24(cdrom),27(sudo),29(audio),44(video),46(plugdev),60(games),100(users),105(input),109(netdev),997(gpio),998(i2c),999(spi)
debug1: client_input_channel_req: channel 0 rtype exit-status reply 0
debug1: client_input_channel_req: channel 0 rtype eow@openssh.com reply 0
debug1: channel 0: free: client-session, nchannels 1
Transferred: sent 2992, received 2892 bytes, in 0.1 seconds
Bytes per second: sent 27756.4, received 26828.7
debug1: Exit status 0

```

# Autostart items

The default uses GNOME autostart<br>
/home/pi/.config/autostart/*

```
pi@raspberrypi:~ $ cat /home/pi/.config/autostart/unitree.desktop 
[Desktop Entry]
Name=unitree
Comment=unitree autostart
Exec=bash /home/pi/UnitreeUpgrade/start.sh
Terminal=false
Type=Application
Categories=System;Utility;Archiving;
StartupNotify=false
NoDisplay=true

pi@raspberrypi:~ $ cat /home/pi/UnitreeUpgrade/start.sh
#!/bin/bash
cd /home/pi/UnitreeUpgrade
python3 ./startup_manager.py  &
python3 ./startup_uploader.py &

cd /home/pi/Unitree/autostart
./update.sh 
```

# PDB emergency shut off (backdoor? no way to disable)
The PDB has an ANNTEM JN1Q on 433mhz hard wired in for safety disconnects. 
https://anntem.aliexpress.com/store/1101246027 (official store)

THe transmitter included is a common 2 button design using a stunted 4 button design "HFY528-4KEY ver2.1".

The HFY528 uses an EV1527 encoder IC by Silvan Chip Electronics www.sc-tech.cn:
```
EV1527 provides individual unique secure ID for each chip. This ID is transmitted with every outgoing packet. The receiver can learn the code 
after receiving the first packet and can be programmed to receive the data from an unique transmitter. This way the communication is secure 
and multiple transmitter can not interfere with the receiver operation. Suitable for operations like digital locks etc. The unique ID is one 
time programmable and is already programmed at the factory. End user applications just need to identify the code and program the receiver to 
communicate with specific IDs.
```

EV1527 and Learning Code Remotes Explained Simple:
https://ripplesecurity.com.au/blogs/news/ev1527-and-ask-explained-simple


You can sniff the remote with rtl_433: 
```
$ rtl_433 -S all -f 433.9M
rtl_433 version 21.05 (2020-05-09) inputs file rtl_tcp RTL-SDR SoapySDR with TLS
Use -h for usage help and see https://triq.org/ for documentation.
Trying conf file at "rtl_433.conf"...
Trying conf file at "/home/ciajeepdoors/.config/rtl_433/rtl_433.conf"...
Trying conf file at "/usr/local/etc/rtl_433/rtl_433.conf"...
Trying conf file at "/etc/rtl_433/rtl_433.conf"...
Registered 157 out of 186 device decoding protocols [ 1-4 8 11-12 15-17 19-23 25-26 29-36 38-60 63 67-71 73-100 102-105 108-116 119 121 124-128 130-149 151-161 163-168 170-175 177-186 ]
Found Fitipower FC0013 tuner
Exact sample rate is: 250000.000414 Hz
Sample rate set to 250000 S/s.
Tuner gain set to Auto.
Tuned to 433.900MHz.
Allocating 15 zero-copy buffers
baseband_demod_FM: low pass filter for 250000 Hz at cutoff 25000 Hz, 40.0 us
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
time      : 2022-07-15 22:47:11
model     : Akhan-100F14 ID (20bit): 0x75ed6
Data (4bit): 0x4 (Mute)
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
time      : 2022-07-15 22:47:11
model     : Akhan-100F14 ID (20bit): 0x75ed6
Data (4bit): 0x4 (Mute)
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
time      : 2022-07-15 22:47:11
model     : Akhan-100F14 ID (20bit): 0x75ed6
Data (4bit): 0x4 (Mute)
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
time      : 2022-07-15 22:47:11
model     : Akhan-100F14 ID (20bit): 0x75ed6
Data (4bit): 0x4 (Mute)
*** Saving signal to file g001_433.9M_250k.cu8 (78818 samples, 262144 bytes)
*** Saving signal to file g002_433.9M_250k.cu8 (35279 samples, 131072 bytes)
*** Saving signal to file g003_433.9M_250k.cu8 (55769 samples, 131072 bytes)
*** Saving signal to file g004_433.9M_250k.cu8 (35280 samples, 131072 bytes)
*** Saving signal to file g005_433.9M_250k.cu8 (35279 samples, 131072 bytes)
*** Saving signal to file g006_433.9M_250k.cu8 (151278 samples, 393216 bytes)
^CSignal caught, exiting!

$ rtl_433 -r g001_433.9M_250k.cu8 -a 4
...
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
time      : @0.415692s
model     : Akhan-100F14 ID (20bit): 0x75ed6
Data (4bit): 0x4 (Mute)
*** signal_start = 58652, signal_end = 122183, signal_len = 63531, pulses_found = 101
Iteration 1. t: 145    min: 59 (45)    max: 231 (56)    delta 18
Iteration 2. t: 145    min: 59 (45)    max: 231 (56)    delta 0
Pulse coding: Short pulse length 59 - Long pulse length 231

Short distance: 111, long distance: 278, packet distance: 2630

p_limit: 145
bitbuffer:: Number of rows: 5 
[00] { 1} 00          : 0
[01] {25} 75 ed 64 00 : 01110101 11101101 01100100 0
[02] {25} 75 ed 64 00 : 01110101 11101101 01100100 0
[03] {25} 75 ed 64 00 : 01110101 11101101 01100100 0
[04] {25} 75 ed 64 00 : 01110101 11101101 01100100 0
Iteration 1. t: 0    min: 0 (0)    max: 0 (0)    delta 3567587328
Iteration 2. t: 0    min: 0 (0)    max: 0 (0)    delta 0
Distance coding: Pulse length 0

Short distance: 1000000, long distance: 0, packet distance: 0

p_limit: 0
bitbuffer:: Number of rows: 0 


```

"Under the developer mode, if the robot is out of control, you can cut off the power of the built-in PDB"<br>

<p align="center">
<img src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/PDB.jpg">
<img src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/remote.png">
<img src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/frame.jpg">
<img src="https://github.com/MAVProxyUser/YushuTechUnitreeGo1/blob/main/warn.jpg">
</p>
<br>

https://www.youtube.com/watch?v=gDnDbuFLjys

# What talks to the STM at 192.168.123.10?

Two apps:
/Unitree/autostart/sportMode/bin/Legged_sport
/Unitree/autostart/appTransit/build/appTransit

```
root@raspberrypi:/home/pi# netstat -ap | grep 192.168.123.10
...
udp     5504      0 192.168.123.161:8008    192.168.123.10:8007     ESTABLISHED 1460/./bin/Legged_s 
udp        0      0 192.168.123.161:8093    192.168.123.10:8007     ESTABLISHED 1752/./build/appTra 

root@raspberrypi:/home/pi# fuser -n udp 8008
8008/udp:             1460
root@raspberrypi:/home/pi# fuser -n udp 8093
8093/udp:             1752
root@raspberrypi:/home/pi# ps -ax | grep 1460 
 1460 ?        SLl    3:08 ./bin/Legged_sport
root@raspberrypi:/home/pi# ps -ax | grep 1752
 1752 ?        Sl     0:02 ./build/appTransit

```

Look familiar? 

https://github.com/unitreerobotics/unitree_legged_sdk/blob/master/include/unitree_legged_sdk/udp.h#L32

```
constexpr int UDP_CLIENT_PORT = 8080;                       // local port
constexpr int UDP_SERVER_PORT = 8007;                       // target port
constexpr char UDP_SERVER_IP_BASIC[] = "192.168.123.10";    // target IP address
constexpr char UDP_SERVER_IP_SPORT[] = "192.168.123.161";   // target IP address
```

# MIT Cheetah code

printf("[Backflip DataReader] Setup for mini cheetah\n");<br>
printf("[Cheetah Test] Test initialization is done\n");<br>

https://github.com/search?q=org%3Amit-biomimetics+%22Cheetah+Test%22&type=code
https://github.com/search?q=org%3Amit-biomimetics+%22Setup+for+mini+cheetah%22&type=code

This code is MIT license. 
https://github.com/mit-biomimetics/Cheetah-Software/blob/master/LICENSE

## Backflip
```

pi@raspberrypi:~/Unitree/autostart/sportMode/path_files $ mv ~/Unitree/autostart/sportMode/path_files/bk_offline_backflip_new_v12.dat ~/Unitree/autostart/sportMode/path_files/offline_backflip_new_v12.dat 
pi@raspberrypi:~/Unitree/autostart/sportMode/path_files $ ls -al
total 232
drwxr-xr-x 2 pi pi   4096 Nov  5  2021 .
drwxr-xr-x 4 pi pi   4096 Nov  5  2021 ..
-rw-r--r-- 1 pi pi 221760 Nov  5  2021 bk_offline_backflip_new_v12.dat
-rwxr-xr-x 1 pi pi    781 Nov  5  2021 pos_w_node.yaml
```

Execute "L1 + Y"<br>

Be careful the dogs hips are weak and will eventually break from stress. Do not over use this feature. 

# Sniffing MQTT traffic on the dog 

Install mosquitto-clients

```
pi@raspberrypi:~ $ sudo apt-get install mosquitto-clients
pi@raspberrypi:~ $ mosquitto_sub -v -t "#"
usys/run ok
usys/uuid xxx-xxx-xxx-xxx-xxx
usys/version/app 1.38.0
usys/version/nano3 
updateDependencies:1.0.1;ipconfig:1.0.0;gencamparams:1.0.0;camerarosnode:1.0.0;03persontrack:2.1.0;imageai:1.0.2;faceLightServer:1.0.1;slamDetector:1.0.0;wsaudio:1.0.0;faceLightMqtt:1.0.0
usys/version/raspi 
updateDependencies:1.0.1;roscore:1.0.0;configNetwork:1.0.0;sportMode:1.38.0;triggerSport:1.5.0;webMonitor:1.4.0;appTransit:1.5.0;07obstacle:1.1.0;utrack:3.9.4;programming:1.0.0;tunnel:1.0.0
usys/version/nano2 
updateDependencies:1.0.1;ipconfig:1.0.0;gencamparams:1.0.0;camerarosnode:1.0.0;03persontrack:2.1.0;imageai:1.0.2;faceLightServer:1.0.1;slamDetector:1.0.0;wsaudio:1.0.0;faceLightMqtt:1.0.0
usys/version/nano1 
updateDependencies:1.0.1;ipconfig:1.0.0;gencamparams:1.0.0;camerarosnode:1.0.0;03persontrack:2.1.0;imageai:1.0.2;faceLightServer:1.0.1;slamDetector:1.0.0;wsaudio:1.0.0;faceLightMqtt:1.0.0
controller/run ok
programming/run on
programming/current_action stop
robot/state ??.??.????.??.??aH?lR??'<M?1??>??>$???#?9?E?:C???
robot/state ??.??.????.??.??aH?lR??'<M?1??>??>$???#?9?E?:C???
robot/state ??.??.????.??.??aH?lR??'<M?1??>??>$???#?9?E?:C???
bms/state 
firmware/version 	%%!$$!$#"$$!$FA
controller/current_action (null)

```

You can also sniff the stick movements. 
```
mosquitto_sub  -h 192.168.12.1 -t "controller/stick" 
```

# Sending MQTT commands to the dog. 

You can send these MQTT commands to control the bot always

```
mosquitto_pub -h 192.168.12.1 -d -t "controller/action" -m "standUp"
mosquitto_pub -h 192.168.12.1 -d -t "controller/action" -m "standDown"
mosquitto_pub -h 192.168.12.1 -d -t "controller/action" -m "run"
mosquitto_pub -h 192.168.12.1 -d -t "controller/action" -m "walk"
mosquitto_pub -h 192.168.12.1 -d -t "controller/action" -m "climb"
```

You must be in SDK mode 2 to send these (L1+L2 & start)
```
mosquitto_pub -h 192.168.12.1 -d -t "controller/action" -m "dance1"
mosquitto_pub -h 192.168.12.1 -d -t "controller/action" -m "dance2"
mosquitto_pub -h 192.168.12.1 -d -t "controller/action" -m "jumpYaw"
mosquitto_pub -h 192.168.12.1 -d -t "controller/action" -m "straightHand1"
```

These commands seem to be somehow black listed on the go1
```
mosquitto_pub -h 192.168.12.1 -d -t "controller/action" -m "backflip"
mosquitto_pub -h 192.168.12.1 -d -t "controller/action" -m "dance3
mosquitto_pub -h 192.168.12.1 -d -t "controller/action" -m "dance4
```

These commands control the stick movement
```
mosquitto_pub -h 192.168.12.1 -d -t "controller/stick" -m <see format below>
```

Stick format is as follows
```
                var c = new Float32Array(4);
                  (c[0] = e.lx),
                  (c[1] = e.rx),
                  (c[2] = e.ry),
                  (c[3] = e.ly),
                  t.publish("controller/stick", c.buffer, { qos: 0 });
```

You can parse stick output with the following code. Ranges go from 1 to -1 with 0 being center. 

```
import paho.mqtt.client as mqtt
import binascii
import struct

def on_connect(client, userdata, flags, rc):
    print("Connected with result code {0}".format(str(rc)))
    client.subscribe("controller/stick")

def on_message(client, userdata, msg):
    [lx,rx,ry,ly] = struct.unpack('ffff', msg.payload)
    print("Message received-> " + msg.topic + " " + str([lx,rx,ry,ly]))

client = mqtt.Client("Stick Data")
client.on_connect = on_connect
client.on_message = on_message
client.connect("192.168.12.1", 1883, 60)
client.loop_forever()
```

This example code will make the dog lay down, stand up, switch to walk mode, and go full speed in one direction for a second before stopping

# TFTP to RTOS

The STM RTOS has tftp enabled for updates. 
./autostart/updateDependencies/update_firmware.py:    atftp = "sleep 5; atftp -p -l " + sys.argv[1] + " 192.168.123.10 --tftp-timeout 10;"


It is assumed to be a variants of IAP over tftp per ST spec
https://www.st.com/resource/en/application_note/an3376-stm32f2x7-inapplication-programming-iap-over-ethernet-stmicroelectronics.pdf

If you tftp to 192.168.161.10, the bot will immediately drop. 

```
pi@raspberrypi:~ $ atftp -g -r "*.bin" 192.168.123.10 69 --trace  --verbose
Trace mode on.
Verbose mode on.
sent RRQ <file: *.bin, mode: octet <>>
received DATA <block: 1, size: 0>
sent ACK <block: 1>
```

# Troubleshooting

If you accidentally delete /etc/hosts, or remove the "localhost" entry, the dog will not stand. 

```
pi@raspberrypi:~ $ journalctl -u nginx.service
-- Reboot --
Jul 11 11:26:56 raspberrypi systemd[1]: Starting A high performance web server and a reverse proxy server...
Jul 11 11:26:58 raspberrypi nginx[676]: nginx: [emerg] host not found in upstream "localhost" in /etc/nginx/sites-enabled/default:11
Jul 11 11:26:58 raspberrypi nginx[676]: nginx: configuration file /etc/nginx/nginx.conf test failed
Jul 11 11:26:58 raspberrypi systemd[1]: nginx.service: Control process exited, code=exited, status=1/FAILURE
Jul 11 11:26:58 raspberrypi systemd[1]: nginx.service: Failed with result 'exit-code'.
Jul 11 11:26:58 raspberrypi systemd[1]: Failed to start A high performance web server and a reverse proxy server.
-- Reboot --
```

General errors can be found in  /home/pi/.cache/lxsession/LXDE-pi/run.log and /home/pi/.ros/log

You can check the status of the system services for degraded stats with 

```
root@raspberrypi:/home/pi# systemctl status
● raspberrypi
    State: degraded
     Jobs: 0 queued
   Failed: 1 units
...

root@raspberrypi:/home/pi# systemctl 
  UNIT                                                                                                LOAD   ACTIVE SUB       DESCRIPTION               
...
● nginx.service                                                                                       loaded failed failed    A high performance web server and a 
reverse proxy server                              
...
pi@raspberrypi:~ $ systemctl list-units --failed
  UNIT          LOAD   ACTIVE SUB    DESCRIPTION                                             
● nginx.service loaded failed failed A high performance web server and a reverse proxy server

```
