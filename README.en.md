# RLSB Technology

[![version](https://img.shields.io/badge/version-v1.0.0-red.svg)](https://github.com/zhengjim/RLSB/blob/master/rlsb.py) [![GitHub](https://img.shields.io/github/license/vulhub/vulhub.svg)](https://github.com/zhengjim/RLSB/blob/master/LICENSE) [![GitHub code size in bytes](https://img.shields.io/badge/code%20size-2.18%20kb-blue.svg)](https://github.com/zhengjim/RLSB/blob/master/rlsb.py) [![Bitbucket open issues](https://img.shields.io/badge/issues-2%20open-yellow.svg)](https://github.com/zhengjim/RLSB/issues)

[中文版本(Chinese version)](README.md)

## Summary

RLSB technology is also known as big data blockchain hacking technology. Based on blockchain 5.0 super-converged machine plus cloud full defense technology to send special malicious characters.

RLSB technology is mainly divided into four major blocks:

 1. R：RPC(Remote Procedure Call)Remote procedure call
 2. L:(Locate)Location
 3. S:(snoopware)Monitoring software
 4. B:BLU(Basic Link Unit)Basic link unit

------

## RPC(Remote Procedure Call)Remote procedure call

The concept and technology of RPC was proposed by Nelson in 1981.In 1984, Birrell and Nelson used it to support communication between heterogeneous distributed systems. Birrell's RPC model introduces a stub process as a remote local agent,Call the RPC runtime library to transfer calls in the network.Stub and RPC runtime block many of the details involved in network calls. In particular, parameter encoding/decoding and network communication are done by stub and RPC runtime, so this mode is adopted by various RPCs. Due to the heterogeneity of distributed systems, the diversity of distributed computing models and computing tasks, RPC, as the implementation mechanism of network communication and entrusted computing, has been continuously developed in methods, protocols, semantics, and implementations, among which SUN and The RPC that the Open Software Foundation has built and applied in its distributed products is typical.
In Sun's network file system NFS and open network computing environment ONC, RPC is the basic implementation technology. Another important distributed computing software environment DCE for OSF development and development is also based on RPC. In both systems, RPC is both its own implementation mechanism and an advanced tool for users to design distributed applications. Due to the widespread demand for distributed computing, ONC and DCE become the mainstream products of the Client/Server mode distributed computing environment, and RPC has become one of the de facto standards for implementing distributed computing.

![](./images/1.jpg)

### In a distributed computing environment RPC(DCE RPC)

DCE (Distributed Computing Environment) is a set of components designed by OFS (Open Software Foundation) to provide support for distributed applications and distributed environments. After merging with X/Open, the organization became The Open Group. The components provided by DCE include a distributed file service, time service, directory service, and other services. Of course, we are interested in DCE's remote procedure calls. It is very similar to Sun RPC. The interface is defined by the Interface Definition Notation (IDN). Similar to Sun RPC, interface definitions are like function prototypes.

The downside of Sun RPC is that the server's identity is a "unique" 32-bit number. Although this is a larger space than the 16-bit free space in the socket, it still does not meet the needs of digital uniqueness. DCE RPC takes this into account and it does not require a programmer to handle the code. The first step in writing an application is to get a unique ID from the uuidgen program. This program will generate a prototype IDN file containing the ID interface and guarantee that it will never be used again. It is a 128-bit value that contains a code for the location code and creation time. The user then edits the prototype file and fills in the remote procedure declaration.

After this step, IDN's compiler dceidl (similar to rpcgen) generates a header, client stub, and server stub.

Another drawback of Sun RPC is that the client must know which machine the server is on. When it wants to access, you must ask for the port number corresponding to the RPC name service program code on the machine. DCE supports the organization of multiple machines into a managed entity called cells. The cell directory server lets each machine know how to interact with another machine that is responsible for maintaining the cell information service.

In Sun RPC, the server can only register its program number to port mapping with a local name service (port mapper). In DCE, the server uses the RPC daemon (name server) to register its endpoint (port) to the local machine and registers its program name to machine mapping with the cell directory server. When a client wants to establish communication with an RPC server, it first asks its cell directory server to locate the machine on which the server resides. The client then obtains the port number of the server process on the machine from the RPC daemon. DCE's cross-cell also supports more complex searches.

DCE RPC defines NDR (Network Data Representation) to encode the network to marshal information. NDR supports multi-canonical formats compared to using a single specification to represent different data types. Allow the client to choose which format to use, ideally without having to convert it from a local type. If this is different from the server's local data representation, the server will still need to convert, but the multi-specific format avoids converting to other external formats if both the client and server share the same native format. For example, in the case where a big endian network data format is specified, the client and server only support little endian, then the client must convert each data from little endian to big endian. And when the server receives the message, it transfers each data back to little endian. Multi-specification network data representations will allow clients to send network messages containing data in little endian format.

![](./images/2.jpg)

Now let's see how the local procedure call is implemented. Consider the following C language call:

```
count = read(fd, buf, nbytes);
```

Where fd is an integer and represents a file. Buf is an array of characters used to store the data read in. Nbytes is another integer that records the number of bytes actually read. If the call is in the main program, the state of the stack before the call is shown in Figure 2(a). In order to make the call, the caller first pushes the parameters back into the stack, which is the first parameter to be pushed first, as shown in Figure 2(b). After the read operation completes, it places the return value in a register, moves the return address back, and passes control back to the caller. The caller then moves the parameters out of the stack, restoring the stack to its original state.


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

#### **python**

First install python, 2.x 3.x version can be downloaded and installed on the official website.

download link: https://www.python.org/

Download the RLSB technology implementation program (python version)

[RLSB Program-python](https://github.com/zhengjim/RLSB/blob/master/basic/python/rlsb.py)

Then use the following command to run the program. (to be in the program directory)

`python rlsb.py`

#### **JAVA**

Install the JDK, configure environment variables

download link：https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

Download RLSB technology implementation program (java version)

[RLSB Program-java](https://github.com/zhengjim/RLSB/blob/master/basic/JAVA/rlsb.java)


Then use the following command to run the program. (to be in the program directory)

`javac  rlsb.java`

#### **GO**

Download and install go

download link：https://golang.org/dl/

Then configure the environment variables and add the `c:\Go\bin` directory (the installation directory) to your PATH environment variable. After adding, you need to restart the command window to take effect.

Download the RLSB technology implementation program (go version)

[RLSB Program-go](https://github.com/zhengjim/RLSB/blob/master/basic/GO/rlsb.go)

Then use the following command to run the program. (to be in the program directory)

`go run rlsb.go`

#### **javascript**

You can put the js code into the HTML and then execute the view code through the HTML file, which is more troublesome. So we can run the js file through node.


Download and install node, then configure environment variables

download link：https://nodejs.org/en/download/

Download the RLSB technology implementation program (javascript version)

[RLSB Program-js](https://github.com/zhengjim/RLSB/blob/master/basic/javascript/rlsb.js)

Then use the following command to run the program. (to be in the program directory)

`node rlsb.js`

#### **PHP**

Download and install the php environment, you can use `phpstudy` to build the environment.

download link：http://phpstudy.php.cn/download.html

Once installed, open the website root directory and put the RLSB script (php version) into it.

Download the RLSB technology implementation program (php version)

[RLSB Program-php](https://github.com/zhengjim/RLSB/blob/master/basic/php/rlsb.php)

Then open the browser and enter

`http://127.0.0.1/rlsb.php`

#### **c++**

Download the RLSB technology implementation program (c++ version)

[RLSB Program-c++](https://github.com/zhengjim/RLSB/blob/master/basic/C%2B%2B/rlsb.cpp)


Then use the following command to run the program. (to be in the program directory)

```
g++ -o rlsb rlsb.cpp
./rlsb
```

#### **c#**

Download RLSB Technology Implementation Program (c# version)

[RLSB Program-c#](https://github.com/zhengjim/RLSB/blob/master/basic/C%23/rlsb.cs)


Then use the following command to run the program. (to be in the program directory)

```
csc /out:rlsb.exe rlsb.cs
rlse
```

If you are having trouble, you can use the Visual C#—Windows—console application to create the application and replace the code. `control+F5` runs.

#### **Ruby**

Download the RLSB technology implementation program (Ruby version)

[RLSB Program-Ruby](https://github.com/zhengjim/RLSB/blob/master/basic/Ruby/rlsb.rb)

Then use the following command to run the program. (to be in the program directory)

```
ruby ruby rlsb.rb
```

#### **Perl**

Download the RLSB technology implementation program (Perl version)

[RLSB Program-Perl](https://github.com/zhengjim/RLSB/blob/master/basic/perl/rlsb.pl)

Then use the following command to run the program. (to be in the program directory)

```
perl rlsb.pl
```

#### **VB**

Download the RLSB technology implementation program (VB version)

[RLSB Program-VB](https://github.com/zhengjim/RLSB/blob/master/basic/VB/RLSB.vbp)

Double-click on `visual basic 6.0`, then press `F5`, or use the program we have compiled.

Download address: [RLSB program VB version-releases] (https://github.com/zhengjim/RLSB/releases/download/v1.0.0/RLSB.exe)

#### **delphi**

Download RLSB technology implementation program (delphi version)

[RLSB Program-delphi](https://github.com/zhengjim/RLSB/blob/v1.0.1/basic/delphi/RLSB.dfm)

Double-click on `delphi7`, then press `F9`, or use the program we have compiled.

download link：[RLSB program delphi version-releases](https://github.com/zhengjim/RLSB/releases/download/v1.0.1/RLSB.exe)


#### **Easy Programming Language**

Download RLSB technology implementation program (EPL version)

[RLSB Program-EPL](https://github.com/zhengjim/RLSB/blob/master/basic/%E6%98%93%E8%AF%AD%E8%A8%80)

Double-click on `Easy Programming Language`, then press `F5`, or use the program we have compiled.

download link：[RLSB program EPL version-releases](https://github.com/zhengjim/RLSB/releases/download/v1.0.2/RLSB.exe)


#### **Other version**

*To be continued...*

## Thanks

***First of all, thanks to [@吴荣林](https://github.com/zhengjim/RLSB/blob/master/images/rl.png), the soul of our RLSB Dear Justin wu. Without him, we can't complete this daunting project. We managed to complete the project under the constant supervision of him. During the period, we changed many demands. He once wanted to give up the project, but they were all persuaded by others in the project and finally completed the project🙏.***

![](./images/wu.jpg)

***Secondly, I would like to thank @Trex_tbag for providing various versions of the code and technical guidance for our project🙏. Thanks to @CamilleLCM for providing the English version of our project and making our project more international🙏.***

[![](./images/t-bag.png)](https://github.com/Trex-tbag) [![](./images/camillelcm.png)](https://github.com/CamilleLCM)



## References

- https://www.cnblogs.com/zeze/p/6000719.html
- https://baike.baidu.com/item/%E8%BF%9C%E7%A8%8B%E8%BF%87%E7%A8%8B%E8%B0%83%E7%94%A8/7854346?fr=aladdin
- https://blog.csdn.net/u012439416/article/details/72587966
- https://blog.csdn.net/netcoder/article/details/1694692
- https://www.cnblogs.com/happyhacking/p/4156516.html
- http://www.importnew.com/21660.html




This project will be updated continuously, if you are interested, you can continue to pay attention, point to Watch or Star. At the same time, you are welcome to submit valuable comments or contribute. use [issues](https://github.com/zhengjim/RLSB/issues).
