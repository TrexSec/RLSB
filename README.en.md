# RLSB Technology

[![version](https://img.shields.io/badge/version-v1.0.0-red.svg)](https://github.com/zhengjim/RLSB/blob/master/rlsb.py) [![GitHub](https://img.shields.io/github/license/vulhub/vulhub.svg)](https://github.com/zhengjim/RLSB/blob/master/LICENSE) [![GitHub code size in bytes](https://img.shields.io/badge/code%20size-2.18%20kb-blue.svg)](https://github.com/zhengjim/RLSB/blob/master/rlsb.py) [![Bitbucket open issues](https://img.shields.io/badge/issues-2%20open-yellow.svg)](https://github.com/zhengjim/RLSB/issues)

[中文版本(Chinese version)](README.md)

## Summary

RLSB technology, also known as big data blockchain hacking technology, is based on blockchain 5.0 super-converged machines and cloud-based full defense technology to send special malicious characters.

RLSB technology is mainly divided into four major blocks:

 1. R:Remote Procedure Call (RPC)
 2. L:Location
 3. S:Snoopware
 4. B:Basic Link Unit (BLU)

------

## RPC(Remote Procedure Call)Remote procedure call

The concept and technology of RPC were first proposed by Nelson in 1981. In 1984, Birrell and Nelson used it to support communication between heterogeneous distributed systems. Birrell's RPC model introduces a stub process as a remote local agent, calling the RPC runtime library to transfer calls in the network. The stub and RPC runtime block many of the details involved in network calls. In particular, parameter encoding/decoding and network communication are handled by the stub and RPC runtime, so this mode is adopted by various RPCs. Due to the heterogeneity of distributed systems and the diversity of distributed computing models and tasks, RPC has been continuously developed in terms of methods, protocols, semantics, and implementations. SUN and the Open Software Foundation have built and applied RPC in their distributed products, making it a typical implementation mechanism for network communication and delegated computing.
In SUN's Network File System (NFS) and the Open Network Computing Environment (ONC), RPC is a fundamental implementation technology. Another important distributed computing software environment, DCE, which was developed by the Open Software Foundation, is also based on RPC. In both systems, RPC is not only its own implementation mechanism but also a high-level tool provided to users for designing distributed applications. Due to the widespread demand for distributed computing, ONC and DCE have become the mainstream products of the client/server model for distributed computing environments, and RPC has become one of the de facto standards for implementing distributed computing.

![](./images/1.jpg)

### In a distributed computing environment RPC(DCE RPC)

DCE (Distributed Computing Environment) is a set of components designed by the Open Software Foundation (OSF) to provide support for distributed applications and environments. After merging with X/Open, the organization became The Open Group. The components provided by DCE include a distributed file service, time service, directory service, and other services. Of course, what we're interested in is DCE's remote procedure call. It is very similar to Sun RPC. The interface is defined by Interface Definition Notation (IDN). Similar to Sun RPC, the interface definition looks like a function prototype.

The drawback of Sun RPC is that the server identification is a "unique" 32-bit number. Although this is a larger space than the 16-bit available space in sockets, it still cannot meet the requirement of unique identification. DCE RPC addresses this issue by not requiring the programmer to handle encoding. The first step in writing an application is to obtain a unique ID from the uuidgen program. This program generates a prototype IDN file containing the ID interface and ensures that it will never be used again. It is a 128-bit value that includes an encoding of the location code and creation time. The user then edits the prototype file and fills in the remote procedure declarations.

After this step, the IDN compiler dceidl (similar to rpcgen) will generate a header file, client stub, and server stub.

Another drawback of Sun RPC is that the client needs to know which machine the server is on. When it wants to access the server, it needs to ask the RPC name service program on the machine to get the port number for the encoded program. DCE supports organizing multiple machines into management entities called cells. The cell directory server enables each machine to know how to interact with another machine responsible for maintaining cell information services.

In Sun RPC, the server can only register its program number to a port mapper using the local name service. In contrast, in DCE, the server uses an RPC daemon (name server) to register its endpoint (port) to the local machine and a cell directory server to register the mapping of the program name to the machine. When a client wants to communicate with an RPC server, it first requests its cell directory server to locate the machine where the server resides. Then the client obtains the port number of the server process from the RPC daemon on the machine. DCE's cross-cell also supports more complex searches.

Correct! The Network Data Representation (NDR) used by DCE RPC is designed to encode data for transmission over the network. Unlike Sun RPC's single specification for representing different data types, NDR supports multi-canonical formats. This allows clients to choose which format to use and ideally avoids the need to convert from local types. However, if this differs from the server's local data representation, the server will still need to perform conversions. For example, if a network data format specifies big-endian byte order and the client and server only support little-endian byte order, the client must convert each data item from little-endian to big-endian before sending the message, and the server must convert each item back to little-endian after receiving it. Multi-canonical network data representation would allow the client to send network messages containing data in the little-endian byte order format.

![](./images/2.jpg)

Let's take a look at how local procedure calls are implemented. Consider the following C language call:

```
count = read(fd, buf, nbytes);
```

Where fd is an integer representing a file, buf is a character array used to store read data, and nbytes is another integer used to record the actual number of bytes read. If this call is located in the main program, the stack's state before the call is shown in Figure 2(a). To make the call, the caller first pushes the parameters in reverse order onto the stack, with the last parameter pushed first, as shown in Figure 2(b). After the read operation is completed, it places the return value in a register, pops the return address, and returns control to the caller. The caller then pops the parameters from the stack, restoring the stack to its initial state.

------

## L:(Locate)Location

1）Antenna unit

    The antenna unit of the GPS signal receiver is the front part of the receiving device. The antenna unit includes a receiving antenna and a preamplifier.

The antenna part may be an omnidirectional vibrator antenna or a small spiral antenna or a microstrip antenna, but from the development trend, the microbe antenna is the most widely used and promising.

    In order to improve the signal strength, a preamplifier (LNA) is generally provided at the rear end of the antenna, and the role of the preamplifier is to be made by a very weak GPS.

The electromagnetic energy conversion of the signal becomes a weak current amplification. The preamplifier is divided into external differential and high-amplifier. Since the heterodyne preamplifier not only has amplification,It also has a frequency conversion function, which converts the high-frequency GPS signal into an intermediate frequency signal, which is beneficial to obtain stable positioning accuracy, so most GPS receivers use a heterodyne antenna unit.

2）Signal channel

    A signal channel is a complex electronic device that combines software and hardware and is a core part of a GPS receiver. Its main function is to capture, track, process and measure satellite signals.

Get the data and information you need to navigate your location. The number of channels varies from 1 to 24 depending on the type of receiver. In general, signal channels are currently relevant,Three types, square type and phase type. A new generation of GPS signal receivers widely use related channels, mainly composed of signal acquisition circuits, pseudo noise tracking loops and carrier tracking loops.

3）Memory

    This is a device in the GPS signal that the receiver will locate the pseudorange, carrier phase measurement, manual measurement data and interpreted satellite ephemeris collected in the field for differential navigation and relative positioning of the measured data.

4）Microprocessor

    The computing portion of the receiver consists of a microprocessor and in-machine software. The in-camera software is provided by the receiver manufacturer to implement data acquisition.An important part of channel self-calibration automation, mainly used for signal acquisition, tracking and positioning calculation. The microprocessor combines the in-machine software for the following calculations and processing:

    (1)After power on, instruct each channel to self-test, and measure, correct and store the delay value of each channel;

    (2)Interpret the satellite ephemeris and calculate the three-dimensional coordinates of the station;

    (3)Calculate the lifting time, azimuth and elevation angle of all satellites from the station positioning coordinates and satellite ephemeris, and provide visual satellite data and satellite working conditions to obtain the best positioning star position and improve positioning accuracy.


![](./images/3.jpg)

------

## S:(snoopware)Monitoring software

    At present, domestic software development has shifted from small MIS system development to relatively large-scale monitoring management software development. For example, various telecommunication network management software, building monitoring software, traffic road monitoring, environmental monitoring of the computer room, and the like. It should be said that monitoring software is very popular in current software companies. As far as personal experience is concerned, I think that the development of these monitoring software has the same development model.

Classification of monitoring software

    Monitoring software can be roughly divided into equipment monitoring and non-device monitoring. Equipment monitoring is generally the monitoring of the operation of communication equipment such as telecommunications or other unattended machinery. The monitoring focuses on the fault condition of the equipment and some performance indicators of the equipment. Non-device monitoring generally refers to monitoring such as traffic roads, network security, buildings, and the environment. The general monitoring of such software focuses on real-life pictures or surrounding areas such as temperature, air quality indicators, etc. The analysis based on the image.

Monitoring software process

    The general monitoring software is divided into three layers, as shown below:

    In the above figure, the data acquisition layer collects the corresponding monitoring information, and the data collected in different industries and different software systems is different because of the purpose of monitoring. But the method of collection is different. For example, the fault collection of the communication device generally increases the hardware module for collecting data in the device itself, and can report the collected data to the database through a fixed communication channel or directly present on the interface. The traffic monitoring of building monitoring uses the PTZ to collect scene images.The database layer is responsible for recording the collected historical data and the configuration data of the interface, etc., which has been easy to query and count.

    The upper interface displays the data collected by the acquisition layer and implements the configuration of the monitoring object. When the configuration information of the device is stored in the database, it is required to directly configure the device. The presentation of the interface generally takes two approaches: the application interface and the web interface. Relatively speaking, the web interface is popular and it is also a development trend.

Monitoring software development function module

    The functions that monitoring software generally implements include configuration management, fault management, performance management, user management, and log management. It depends on the needs of the user and the software system itself.

    Configuration management is to implement the configuration of management objects. Requires unique identification of each management element.

    Fault management and performance management are basic functions that require accurate location and fast fault location. And can view the performance status of the managed object. For non-device monitoring software, it is required to accurately and quickly collect data such as pictures that the user wants to view.

    User management is mainly to restrict users from illegal or unauthorized use of the monitoring software system. Users need to be leveld and set their permissions.

    Log management mainly records the important operations of the user on the software system.

## B:BLU(Basic Link Unit)Basic link unit

### Directly connected network:

Point-to-point network: A special medium. One-way, half-duplex, full-duplex.

Multiple access network: Shared media. Broadcast, collision. Unicast, multicast, broadcast.



### Indirectly connected network.

Network interconnection: The interconnection network (internetwork or internet) is composed of a network connected by a router (or gateway). The Internet is an interconnected network. System domain network, local area network, metropolitan area network, wide area network.



### What is the Internet:

Terminal system: Host (running web application).

Communication links: fiber, copper, radio, satellite. Transmission rate = bandwidth.

router.


### The structure of the Internet:

The top ISP is also known as the backbone. A Layer 2 ISP is a smaller ISP (often a regional ISP) that is a top-level ISP customer that can connect to a top-level ISP or other Layer 2 ISP. The terminal system is connected to the Internet through an ISP network (access network). Note: ISP (Internet Service Provider) Internet Service Provider.


### Services provided by the network:

Reliable service: file transfer, web browsing, email, e-commerce

Unreliable services: live video, IP telephony, web conferencing

Connection-oriented service connectionless service

Confirmed service Unconfirmed service

Datagram Service: No connection, no confirmation

Request response and message flow service


### What is an agreement?

A protocol defines rules for transmitting messages between network entities, such as message format, the order in which messages are sent and received.



Network hierarchy
Why is the network layered? Modularity simplifies system maintenance and modification. Each layer of service is implemented through the services provided by the lower layers and the functions of this layer.

### Internet architecture:

Application layer application: Provides support for some specialized applications File Service (FTP), Mail (SMTP), Web Page (HTTP)

Transport layer transport: Data transfer between processes (end-to-end) TCP, UDP

Network layer: The datagram is transmitted from the source host to the destination host (host to host) by routing. IP, routing protocols

Data link layer data link: Data transfer in the physical network (hop to hop, node to node) PPP, Ethernet

Physical layer: the bits on the line (transport the original bit stream)

Encapsulation (encaptualtion):

The data units transmitted by each layer are called packets, and they all belong to a certain protocol, also called a protocol data unit.

------


## Code achieve

The basic version is provided first, and the profssion version will be developed later.

### **BASIC版**

#### **1.python**

First install python, 2.x 3.x version can be downloaded and installed on the official website.

download link: https://www.python.org/

Download the RLSB technology implementation program (python version)

[RLSB Program-python](https://github.com/zhengjim/RLSB/blob/master/basic/python/rlsb.py)

Then use the following command to run the program. (to be in the program directory)

`python rlsb.py`

#### **2.JAVA**

Install the JDK, configure environment variables

download link：https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

Download RLSB technology implementation program (java version)

[RLSB Program-java](https://github.com/zhengjim/RLSB/blob/master/basic/JAVA/rlsb.java)


Then use the following command to run the program. (to be in the program directory)

`javac  rlsb.java`

#### **3.GO**

Download and install go

download link：https://golang.org/dl/

Then configure the environment variables and add the `c:\Go\bin` directory (the installation directory) to your PATH environment variable. After adding, you need to restart the command window to take effect.

Download the RLSB technology implementation program (go version)

[RLSB Program-go](https://github.com/zhengjim/RLSB/blob/master/basic/GO/rlsb.go)

Then use the following command to run the program. (to be in the program directory)

`go run rlsb.go`

#### **4.javascript**

You can put the js code into the HTML and then execute the view code through the HTML file, which is more troublesome. So we can run the js file through node.


Download and install node, then configure environment variables

download link：https://nodejs.org/en/download/

Download the RLSB technology implementation program (javascript version)

[RLSB Program-js](https://github.com/zhengjim/RLSB/blob/master/basic/javascript/rlsb.js)

Then use the following command to run the program. (to be in the program directory)

`node rlsb.js`

#### **5.PHP**

Download and install the php environment, you can use `phpstudy` to build the environment.

download link：http://phpstudy.php.cn/download.html

Once installed, open the website root directory and put the RLSB script (php version) into it.

Download the RLSB technology implementation program (php version)

[RLSB Program-php](https://github.com/zhengjim/RLSB/blob/master/basic/php/rlsb.php)

Then open the browser and enter

`http://127.0.0.1/rlsb.php`

#### **6.c++**

Download the RLSB technology implementation program (c++ version)

[RLSB Program-c++](https://github.com/zhengjim/RLSB/blob/master/basic/C%2B%2B/rlsb.cpp)


Then use the following command to run the program. (to be in the program directory)

```
g++ -o rlsb rlsb.cpp
./rlsb
```

#### **7.c#**

Download RLSB Technology Implementation Program (c# version)

[RLSB Program-c#](https://github.com/zhengjim/RLSB/blob/master/basic/C%23/rlsb.cs)


Then use the following command to run the program. (to be in the program directory)

```
csc /out:rlsb.exe rlsb.cs
rlse
```

If you are having trouble, you can use the Visual C#—Windows—console application to create the application and replace the code. `control+F5` runs.

#### **8.Ruby**

Download the RLSB technology implementation program (Ruby version)

[RLSB Program-Ruby](https://github.com/zhengjim/RLSB/blob/master/basic/Ruby/rlsb.rb)

Then use the following command to run the program. (to be in the program directory)

```
ruby ruby rlsb.rb
```

#### **9.Perl**

Download the RLSB technology implementation program (Perl version)

[RLSB Program-Perl](https://github.com/zhengjim/RLSB/blob/master/basic/perl/rlsb.pl)

Then use the following command to run the program. (to be in the program directory)

```
perl rlsb.pl
```

#### **10.VB**

Download the RLSB technology implementation program (VB version)

[RLSB Program-VB](https://github.com/zhengjim/RLSB/blob/master/basic/VB/RLSB.vbp)

Double-click on `visual basic 6.0`, then press `F5`, or use the program we have compiled.

Download address: [RLSB program VB version-releases] (https://github.com/zhengjim/RLSB/releases/download/v1.0.0/RLSB.exe)

#### **11.delphi**

Download RLSB technology implementation program (delphi version)

[RLSB Program-delphi](https://github.com/zhengjim/RLSB/blob/v1.0.1/basic/delphi/RLSB.dfm)

Double-click on `delphi7`, then press `F9`, or use the program we have compiled.

download link：[RLSB program delphi version-releases](https://github.com/zhengjim/RLSB/releases/download/v1.0.1/RLSB.exe)


#### **12.Easy Programming Language**

Download RLSB technology implementation program (EPL version)

[RLSB Program-EPL](https://github.com/zhengjim/RLSB/blob/master/basic/%E6%98%93%E8%AF%AD%E8%A8%80)

Double-click on `Easy Programming Language`, then press `F5`, or use the program we have compiled.

download link：[RLSB program EPL version-releases](https://github.com/zhengjim/RLSB/releases/download/v1.0.2/RLSB.exe)

#### **13.TCL**

If it's linux, install TCL directly. The installation commands are as follows:

ubuntu
```apt-get install tcl```
centos
```yum install tcl```

If in Windows, you need to install `WinGW'.

Download the RLSB technology implementation program (TCL version)

[RLSB Program-TCL](https://github.com/zhengjim/RLSB/blob/master/basic/TCL/rlsb.tcl)

Then use the following command to run the program. (to be in the program directory)

```
tclsh rlsb.tcl
```


#### **Other version**

*To be continued...*

## Thanks

***First of all, thanks to [@吴荣林](https://github.com/zhengjim/RLSB/blob/master/images/rl.png), the soul of our RLSB Dear Justin wu. Without him, we can't complete this daunting project. We managed to complete the project under the constant supervision of him. During the period, we changed many demands. He once wanted to give up the project, but they were all persuaded by others in the project and finally completed the project🙏.***

![](./images/wu.jpg)

***Secondly, I would like to thank @deFming for providing various versions of the code and technical guidance for our project🙏. Thanks to @CamilleLCM for providing the English version of our project and making our project more international🙏.***

[![](./images/t-bag.png)](https://github.com/deFming) [![](./images/camillelcm.png)](https://github.com/CamilleLCM)


## TODO

- [x] Complete RLSB Technology Basic

- [ ] Complete RLSB Technology profession

- [ ] Bringing RLSB technology to the world


## References

- https://www.cnblogs.com/zeze/p/6000719.html
- https://baike.baidu.com/item/%E8%BF%9C%E7%A8%8B%E8%BF%87%E7%A8%8B%E8%B0%83%E7%94%A8/7854346?fr=aladdin
- https://blog.csdn.net/u012439416/article/details/72587966
- https://blog.csdn.net/netcoder/article/details/1694692
- https://www.cnblogs.com/happyhacking/p/4156516.html
- http://www.importnew.com/21660.html




This project will be updated continuously, if you are interested, you can continue to pay attention, point to Watch or Star. At the same time, you are welcome to submit valuable comments or contribute. use [issues](https://github.com/zhengjim/RLSB/issues).
