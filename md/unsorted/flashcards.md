---
created: 1664724954747
desc: ''
id: 3kxjozddtmps0ljk7bu7txc
title: Flashcards
updated: 1664728297310
---
   
## What do you need in order to communicate?   
   
   
- A common language (for the two ends to understand)   
- A way to address who do you want to communicate with   
- A Connection (so the content of the communication can reach the recipients)   
   
## What is TCP/IP?   
   
A set of protocols that define how two or more devices can communicate with each other.   
To learn more about TCP/IP, read [here](http://www.penguintutor.com/linux/basic-network-reference)   
   
## What is APIPA?   
   
APIPA is a set of it addresses that devices are allocated   
when the main DHCP server is not reachable   
   
## What ip range does APIPA use?   
   
APIPA uses the ip range: 169.254.0.1 - 169.254.255.254.   
   
## What is Ethernet?   
   
Ethernet simply refers to the most common type of Local Area Network (LAN) used today. A LAN—in contrast to a WAN (Wide Area Network), which spans a larger geographical area—is a connected network of computers in a small area, like your office, college campus, or even home.   
   
## What is a MAC address? What is it used for?   
   
A MAC address is a unique identification number or code used to identify individual devices on the network.   
   
Packets that are sent on the ethernet are always coming from a MAC address and sent to a MAC address. If a network adapter is receiving a packet, it is comparing the packet’s destination MAC address to the adapter’s own MAC address.   
   
## When is this MAC address used?: ff:ff:ff:ff:ff:ff   
   
When a device sends a packet to the broadcast MAC address (FF:FF:FF:FF:FF:FF​), it is delivered to all stations on the local network. Ethernet broadcasts are used to resolve IP addresses to MAC addresses (by ARP) at the datalink layer .   
   
## What is an IP address?   
   
An Internet Protocol address (IP address) is a numerical label assigned to each device connected to a computer network that uses the Internet Protocol for communication.An IP address serves two main functions: host or network interface identification and location addressing.   
   
## Explain subnet mask and given an example   
   
A Subnet mask is a 32-bit number that masks an IP address, and divides the IP address into network address and host address. Subnet Mask is made by setting network bits to all "1"s and setting host bits to all "0"s. Within a given network, two host addresses are reserved for special purpose, and cannot be assigned to hosts. The "0" address is assigned a network address and "255" is assigned to a broadcast address, and they cannot be assigned to hosts.   
   
**For Example**   
   
```
| Address Class | No of Network Bits | No of Host Bits | Subnet mask     | CIDR notation |
| ------------- | ------------------ | --------------- | --------------- | ------------- |
| A             | 8                  | 24              | 255.0.0.0       | /8            |
| A             | 9                  | 23              | 255.128.0.0     | /9            |
| A             | 12                 | 20              | 255.240.0.0     | /12           |
| A             | 14                 | 18              | 255.252.0.0     | /14           |
| B             | 16                 | 16              | 255.255.0.0     | /16           |
| B             | 17                 | 15              | 255.255.128.0   | /17           |
| B             | 20                 | 12              | 255.255.240.0   | /20           |
| B             | 22                 | 10              | 255.255.252.0   | /22           |
| C             | 24                 | 8               | 255.255.255.0   | /24           |
| C             | 25                 | 7               | 255.255.255.128 | /25           |
| C             | 28                 | 4               | 255.255.255.240 | /28           |
| C             | 30                 | 2               | 255.255.255.252 | /30           |

```
   
   
## What is a private IP address? In which scenarios/system designs, one should use it?   
   
Private IP addresses are assigned to the hosts in the same network to communicate among one another. As the name "private" suggests, the devices having the private IP addresses assigned can't be reached by the devices from any external network. For example, if I am living in a hostel and I want my hostelmates to join the game server I have hosted, I will ask them to join via my server's private IP address, since the network is local to the hostel.   
   
## What is a public IP address? In which scenarios/system designs, one should use it?   
   
A public IP address is the public facing IP address. In the event that you was hosting a game server that you want your friends to join, you will give your friends your public IP address to allow their computers to identify and locate your network and server in order for the connection to take place. One time that you would not need to use a public facing IP address is in the event that you was playing with friends who was connected to the same network as you, in that case, you would use a private ip address. In order for someone to be able to connect to your server that is located internally, you will have to setup a port forward to tell your router to allow traffic from the public domain into your network and vice versa.   
   
## Explain the OSI model. What layers there are? What each layer is responsible for?   
   
   
- Application: user end (HTTP is here)   
- Presentation: establishes context between application-layer entities (Encryption is here)   
- Session: establishes, manages and terminates the connections   
- Transport: transfers variable-length data sequences from a source to a destination host (TCP & UDP are here)   
- Network: transfers datagrams from one network to another (IP is here)   
- Data link: provides a link between two directly connected nodes (MAC is here)   
- Physical: the electrical and physical spec the data connection (Bits are here)   
   
You can read more about the OSI model in [penguintutor.com](http://www.penguintutor.com/linux/basic-network-reference)   
   
## For each of the following determine to which OSI layer it belongs:   
   
   
- Error correction   
- Packets routing   
- Cables and electrical signals   
- MAC address   
- IP address   
- Terminate connections   
- 3 way handshake   
   
   
- Error correction - Data link   
- Packets routing - Network   
- Cables and electrical signals - Physical   
- MAC address - Data link   
- IP address - Network   
- Terminate connections - Session   
- 3 way handshake - Transport   
   
## What delivery schemes are you familiar with?   
   
Unitcast: One to one communication where there is one sender and one receiver.   
   
Broadcast: Sending a message to everyone in the network. The address ff:ff:ff:ff:ff:ff is used for broadcasting.   
Two common protocols which use broadcast are ARP and DHCP.   
   
Multicast: Sending a message to a group of subscribers. It can be one-to-many or many-to-many.   
   
## What is CSMA/CD? Is it used in modern ethernet networks?   
   
CSMA/CD stands for Carrier Sense Multiple Access / Collision Detection.   
Its primarily focus it to manage access to shared medium/bus where only one host can transmit at a given point of time.   
   
CSMA/CD algorithm:   
   
1. Before sending a frame, it checks whether another host already transmitting a frame.   
2. If no one transmitting, it starts transmitting the frame.   
3. If two hosts transmitted at the same time, we have a collision.   
4. Both hosts stop sending the frame and they send to everyone a 'jam signal' notifying everyone that a collision occurred   
5. They are waiting for a random time before sending again   
6. Once each host waited for a random time, they try to send the frame again and so the   
   
## Describe the following network devices and the difference between them:   
   
   
- router   
- switch   
- hub   
   
## What is a "Collision Domain"?   
   
## What is a "Broadcast Domain"?   
   
## three computers connected to a switch. How many collision domains are there? How many broadcast domains?   
   
Three collision domains and one broadcast domain   
   
## How does a router works?   
   
A router is a physical or virtual appliance that passes information between two or more packet-switched computer networks. A router inspects a given data packet's destination Internet Protocol address (IP address), calculates the best way for it to reach its destination and then forwards it accordingly.   
   
## What is NAT?   
   
Network Address Translation (NAT) is a process in which one or more local IP address is translated into one or more Global IP address and vice versa in order to provide Internet access to the local hosts.   
   
## What is a proxy? How does it works? What do we need it for?   
   
A proxy server acts as a gateway between you and the internet. It’s an intermediary server separating end users from the websites they browse.   
   
If you’re using a proxy server, internet traffic flows through the proxy server on its way to the address you requested. The request then comes back through that same proxy server (there are exceptions to this rule), and then the proxy server forwards the data received from the website to you.   
   
Proxy servers provide varying levels of functionality, security, and privacy depending on your use case, needs, or company policy.   
   
## What is TCP? How does it works? What is the 3 way handshake?   
   
TCP 3-way handshake or three-way handshake is a process which is used in a TCP/IP network to make a connection between server and client.   
   
A three-way handshake is primarily used to create a TCP socket connection. It works when:   
   
   
- A client node sends a SYN data packet over an IP network to a server on the same or an external network. The objective of this packet is to ask/infer if the server is open for new connections.   
- The target server must have open ports that can accept and initiate new connections. When the server receives the SYN packet from the client node, it responds and returns a confirmation receipt – the ACK packet or SYN/ACK packet.   
- The client node receives the SYN/ACK from the server and responds with an ACK packet.   
   
## What is round-trip delay or round-trip time?   
   
From [wikipedia](https://en.wikipedia.org/wiki/Round-trip_delay): "the length of time it takes for a signal to be sent plus the length of time it takes for an acknowledgement of that signal to be received"   
   
Bonus question: what is the RTT of LAN?   
   
## How does SSL handshake work?   
   
## What is the difference between TCP and UDP?   
   
TCP establishes a connection between the client and the server to guarantee the order of the packages, on the other hand, UDP does not establish a connection between client and server and doesn't handle package order. This makes UDP more lightweight than TCP and a perfect candidate for services like streaming.   
   
[Penguintutor.com](http://www.penguintutor.com/linux/basic-network-reference) provides a good explanation.   
   
## What TCP/IP protocols are you familiar with?   
   
## Explain "default gateway"   
   
A default gateway serves as an access point or IP router that a networked computer uses to send information to a computer in another network or the internet.   
   
## What is ARP? How does it works?   
   
ARP stands for Address Resolution Protocol. When you try to ping an IP address on your local network, say 192.168.1.1, your system has to turn the IP address 192.168.1.1 into a MAC address. This involves using ARP to resolve the address, hence its name.   
   
Systems keep an ARP look-up table where they store information about what IP addresses are associated with what MAC addresses. When trying to send a packet to an IP address, the system will first consult this table to see if it already knows the MAC address. If there is a value cached, ARP is not used.   
   
## What is TTL? What does it helps to prevent?   
   
## What is DHCP? How does it works?   
   
It stands for Dynamic Host Configuration Protocol, and allocates IP addresses, subnet masks and gateways to hosts. This is how it works:   
   
   
- A host upon entering a network, broadcasts a message in search of a DHCP server (DHCP DISCOVER)   
- An offer message is sent back by the DHCP server as a packet containing lease time, subnet mask, IP addresses, etc (DHCP OFFER)   
- Depending on which offer accepted, the client sends back a reply broadcast letting all DHCP servers know (DHCP REQUEST)   
- Server sends an acknowledgment (DHCP ACK)   
   
Read more [here](https://linuxjourney.com/lesson/dhcp-overview)   
   
## Can you have two DHCP servers in the same network? How it works?   
   
## What is SSL tunneling? How does it works?   
   
## What is a socket? Where can you see the list of sockets in your system?   
   
## What is IPv6? Why should we consider using it if we have IPv4?   
   
## What is VLAN?   
   
## What is MTU?   
   
MTU stands for Maximum Transmission Unit. It's the size of the largest PDU (protocol Data Unit) that can be sent in a single transaction.   
   
## What happens if you send a packet that is bigger than the MTU?   
   
With IPv4 protocol, router can fragment the PDU then sending all the fragmented PDU through the transaction.   
With IPv6 protocol, it issues a error to the user's computer.   
   
## True or False?. Ping is using UDP because it doesn't care about reliable connection   
   
## What is SDN?   
   
## What is ICMP? What is it used for?   
   
## What is NAT? How does it work?   
   
NAT stands for network address translation. It’s a way to map multiple local private addresses to a public one before transferring the information. Organizations that want multiple devices to employ a single IP address use NAT, as do most home routers.   
For example, your computer's private IP could be 192.168.1.100, but your router maps the traffic to it's public IP (e.g. 1.1.1.1). Any device on the internet would see the traffic coming from your public IP (1.1.1.1) instead of your private IP (192.168.1.100).   
   
## Which factors affect network performances   
   
## Which port number is used in each of the following protocols?:   
   
   
- SSH   
- SMTP   
- HTTP   
- DNS   
- HTTPS   
- FTP   
- SFTP   
   
   
- SSH - 22   
- SMTP - 25   
- HTTP - 80   
- DNS - 53   
- HTTPS - 443   
- FTP - 21   
- SFTP - 22   
   
## Which factors affect network performances   
   
#### Network - Data and Control planes   
   
## What "control plane" refers to?   
   
The control plane is the part of the network that decides how to route and forward packets to a different location.   
   
## What "data plane" refers to?   
   
The data plane is the part of the network that actually forwards the data/packets.   
   
## What "management plane" refers to?   
   
Refers to monitoring and management functions.   
   
## To which plane (data, control, ...) is creating routing tables belongs to?   
   
Control Plane.   
   
## Explain Spanning Tree Protocol (STP)   
   
## What is link aggregation? Why is it used?   
   
## What is Asymmetric Routing? How do deal with it?   
   
## What overlay (tunnel) protocols are you familiar with?   
   
## What is GRE? How does it works?   
   
## What is VXLAN? How does it works?   
   
## What is SNAT?   
   
## Explain OSPF   
   
## What is latency?   
   
Latency is the time taken for an information to reach its destination from the source.   
   
## What is bandwidth?   
   
Bandwidth is the capacity of a communication channel to measure how much data the latter can handle over a specific time period. More bandwidth would imply more traffic handling and thus more data transfer.   
   
## What is throughput?   
   
Throughput refers to the measurement of the real amount of data transferred over a certain period of time across any transmission channel.   
   
## When performing a search query, what is more important, latency or throughput? And how to assure that what managing global infrastructure?   
   
Latency. To have a good latency, a search query should be forwarded to the closest datacenter.   
   
## When uploading a video, what is more important, latency or throughput? And how to assure that?   
   
Throughput. To have a good throughput, the upload stream should be routed to an underutilized link.   
   
## What other considerations (except latency and throughput) are there when forwarding requests?   
   
   
- Keep caches updated (which means the request could be forwarded not to the closest datacenter)   
   
## Explain Spine & Leaf   
   
## What is Network Congestion? What can cause it?   
   
## What can you tell me about UDP packet format? What about TCP packet format? How is it different?   
   
## What is the exponential backoff algorithm? Where is it used?   
   
## Using Hamming code, what would be the code word for the following data word 100111010001101?   
   
00110011110100011101   
   
## Give examples of protocols found in the application layer   
   
   
- Hypertext Transfer Protocol (HTTP) - used for the webpages on the internet   
- Simple Mail Transfer Protocol (SMTP) - email transmission   
- Telecommunications Network - (TELNET) - terminal emulation to allow client access to telnet server   
- File Transfer Protocol (FTP) - facilitates transfer of files between any two machines   
- Domain Name System (DNS) - domain name translation   
- Dynamic Host Configuration Protocol (DHCP) - allocates IP addresses, subnet masks and gateways to hosts   
- Simple Network Management Protocol (SNMP) - gathers data of devices on the network   
   
## Give examples of protocols found in the network Layer   
   
   
- Internet Protocol (IP) - assists in routing packets from one machine to another   
- Internet Control Message Protocol (ICMP) - lets one know what is going such as error messages and debugging information   
   
## What is HSTS?   
   
HTTP Strict Transport Security is a web server directive that informs user agents and web browsers how to handle its connection through a response header sent at the very beginning and back to the browser. This forces connections over HTTPS encryption, disregarding any script's call to load any resource in that domain over HTTP.   
   
Read more [here](https://www.globalsign.com/en/blog/what-is-hsts-and-how-do-i-use-it#:~:text=HTTP%20Strict%20Transport%20Security%20(HSTS,and%20back%20to%20the%20browser.)   
   
## What is the Internet? Is it the same as the World Wide Web?   
   
The internet refers to network of networks, transferring huge amounts of data around the globe.<br>   
The World Wide Web is an application running on millions of server, on top of the internet, accessed through what is know as the web browser   
   
## What is the ISP?   
   
ISP (Internet Service Provider) is the local internet company provider.   
   
   
---   
   
## What is an operating system?   
   
From the book "Operating Systems: Three Easy Pieces":   
   
"responsible for making it easy to run programs (even allowing you to seemingly run many at the same time), allowing programs to share memory, enabling programs to interact with devices, and other fun stuff like that".   
   
## Can you explain what is a process?   
   
A process is a running program. A program is one or more instructions and the program (or process) is executed by the operating system.   
   
## If you had to design an API for processes in an operating system, what would this API look like?   
   
It would support the following:   
   
   
- Create - allow to create new processes   
- Delete - allow to remove/destroy processes   
- State - allow to check the state of the process, whether it's running, stopped, waiting, etc.   
- Stop - allow to stop a running process   
   
## How a process is created?   
   
   
- The OS is reading program's code and any additional relevant data   
- Program's code is loaded into the memory or more specifically, into the address space of the process.   
- Memory is allocated for program's stack (aka run-time stack). The stack also initialized by the OS with data like argv, argc and parameters to main()   
- Memory is allocated for program's heap which is required for dynamically allocated data like the data structures linked lists and hash tables   
- I/O initialization tasks are performed, like in Unix/Linux based systems where each process has 3 file descriptors (input, output and error)   
- OS is running the program, starting from main()   
   
## True or False? The loading of the program into the memory is done eagerly (all at once)   
   
False. It was true in the past but today's operating systems perform lazy loading which means only the relevant pieces required for the process to run are loaded first.   
   
## What are different states of a process?   
   
   
- Running - it's executing instructions   
- Ready - it's ready to run but for different reasons it's on hold   
- Blocked - it's waiting for some operation to complete. For example I/O disk request   
   
## What are some reasons for a process to become blocked?   
   
   
- I/O operations (e.g. Reading from a disk)   
- Waiting for a packet from a network   
   
## What is Inter Process Communication (IPC)?   
   
## What is "time sharing"?   
   
Even when using a system with one physical CPU, it's possible to allow multiple users to work on it and run programs. This is possible with time sharing where computing resources are shared in a way it seems to the user the system has multiple CPUs but in fact it's simply one CPU shared by applying multiprogramming and multi-tasking.   
   
## What is "space sharing"?   
   
Somewhat the opposite of time sharing. While in time sharing a resource is used for a while by one entity and then the same resource can be used by another resource, in space sharing the space is shared by multiple entities but in a way where it's not being transferred between them.<br>   
It's used by one entity until this entity decides to get rid of it. Take for example storage. In storage, a file is yours until you decide to delete it.   
   
## What component determines which process runs at a given moment in time?   
   
CPU scheduler   
   
## What is "virtual memory" and what purpose it serves?   
   
Virtual memory combines your computer's RAM with temporary space on your hard disk. When RAM runs low, virtual memory helps to move data from RAM to a space called a paging file. Moving data to paging file can free up the RAM so your computer can complete its work. In general, the more RAM your computer has, the faster the programs run.   
[https://www.minitool.com/lib/virtual-memory.html](https://www.minitool.com/lib/virtual-memory.html)   
   
## What is demand paging?   
   
## What is copy-on-write or shadowing?   
   
## What is a kernel, and what does it do?   
   
The kernel is part of the operating system and is responsible for tasks like:   
   
   
- Allocating memory   
- Schedule processes   
- Control CPU   
   
## True or False? Some pieces of the code in the kernel are loaded into protected areas of the memory so applications can't overwritten them   
   
True   
   
## What is POSIX?   
   
## Explain what is Semaphore and what its role in operating systems   
   
## What is cache? What is buffer?   
   
Buffer: Reserved place in RAM which is used to hold data for temporary purposes   
Cache: Cache is usually used when processes reading and writing to the disk to make the process faster by making similar data used by different programs easily accessible.   
   
   
---   
   
## What is Virtualization?   
   
Virtualization uses software to create an abstraction layer over computer hardware that allows the hardware elements of a single computer—processors, memory, storage and more - to be divided into multiple virtual computers, commonly called virtual machines (VMs).   
   
## What is a hypervisor?   
   
Red Hat: "A hypervisor is software that creates and runs virtual machines (VMs). A hypervisor, sometimes called a virtual machine monitor (VMM), isolates the hypervisor operating system and resources from the virtual machines and enables the creation and management of those VMs."   
   
Read more [here](https://www.redhat.com/en/topics/virtualization/what-is-a-hypervisor)   
   
## What types of hypervisors are there?   
   
Hosted hypervisors and bare-metal hypervisors.   
   
## What are the advantages and disadvantges of bare-metal hypervisor over a hosted hypervisor?   
   
Due to having its own drivers and a direct access to hardware components, a baremetal hypervisor will often have better performances along with stability and scalability.   
   
On the other hand, there will probably be some limitation regarding loading (any) drivers so a hosted hypervisor will usually benefit from having a better hardware compatibility.   
   
## What types of virtualization are there?   
   
Operating system virtualization   
Network functions virtualization   
Desktop virtualization   
   
## Is containerization is a type of Virtualization?   
   
Yes, it's a operating-system-level vip[rtualization, where the kernel is shared and allows to use multiple isolated user-spaces instances.   
   
## How the introduction of virtual machines changed the industry and the way applications were deployed?   
   
The introduction of virtual machines allowed companies to deploy multiple business applications on the same hardware while each application is separated from each other in secured way, where each is running on its own separate operating system.   
   
## Do we need virtual machines in the age of containers? Are they still relevant?   
   
   
---   
   
## Explain inheritance and how to use it in Python   
   
## Explain and demonstrate class attributes & instance attributes   
   
In the following block of code `x` is a class attribute while `self.y` is a instance attribute   
   
```
class MyClass(object):
    x = 1

    def __init__(self, y):
        self.y = y
```
   
   
#### Python - Exceptions   
   
## What is an error? What is an exception? What types of exceptions are you familiar with?   
   
```
#  Note that you generally don't need to know the compiling process but knowing where everything comes from
#  and giving complete answers shows that you truly know what you are talking about.

Generally, every compiling process have a two steps.
    - Analysis
    - Code Generation.

    Analysis can be broken into:
        1. Lexical analysis   (Tokenizes source code)
        2. Syntactic analysis (Check whether the tokens are legal or not, tldr, if syntax is correct)

               for i in 'foo'
                          ^
             SyntaxError: invalid syntax

        We missed ':'


        3. Semantic analysis  (Contextual analysis, legal syntax can still trigger errors, did you try to divide by 0,
          hash a mutable object or use an undeclared function?)

                 1/0
                ZeroDivisionError: division by zero

    These three analysis steps are the responsible for error handlings.

    The second step would be responsible for errors, mostly syntax errors, the most common error.
    The third step would be responsible for Exceptions.

    As we have seen, Exceptions are semantic errors, there are many builtin Exceptions:

        ImportError
        ValueError
        KeyError
        FileNotFoundError
        IndentationError
        IndexError
        ...

    You can also have user defined Exceptions that have to inherit from the `Exception` class, directly or indirectly.

    Basic example:

    class DividedBy2Error(Exception):
        def __init__(self, message):
            self.message = message


    def division(dividend,divisor):
        if divisor == 2:
            raise DividedBy2Error('I dont want you to divide by 2!')
        return dividend / divisor

    division(100, 2)

    >>> __main__.DividedBy2Error: I dont want you to divide by 2!
```
   
   
## Explain Exception Handling and how to use it in Python   
   
**Exceptions:** Errors detected during execution are called Exceptions.   
   
**Handling Exception:** When an error occurs, or exception as we call it, Python will normally stop and generate an error message.</br>   
Exceptions can be handled using `try` and `except` statement in python.   
   
**Example:** Following example asks the user for input until a valid integer has been entered. </br>   
If user enter a non-integer value it will raise exception and using except it will catch that exception and ask the user to enter valid integer again.   
   
```py
while True:
    try:
        a = int(input("please enter an integer value: "))
        break
    except ValueError:
        print("Ops! Please enter a valid integer value.")

```
   
   
For more details about errors and exceptions follow this [https://docs.python.org/3/tutorial/errors.html](https://docs.python.org/3/tutorial/errors.html)   
   
## What is the result of running the following function?   
   
```
def true_or_false():
    try:
        return True
    finally:
        return False
```
   
   
False   
   
#### Python Built-in functions   
   
## Explain the following built-in functions (their purpose + use case example):   
   
   
- repr   
- any   
- all   
   
## What is the difference between repr function and str?   
   
## What is the **call** method?   
   
It is used to emulate callable objects. It allows a class instance to be called as a function.   
   
   
- Example code:   
   
```
class Foo:
    def __init__(self: object) ->  None:
        pass
    def __call__(self: object) -> None:
        print("Called!")

f = Foo()
f()
```
   
   
   
- Result:   
   
```
Called!
```
   
   
## Do classes has the **call** method as well? What for?   
   
## What \_ is used for in Python?   
   
1. Translation lookup in i18n   
2. Hold the result of the last executed expression or statement in the interactive interpreter.   
3. As a general purpose "throwaway" variable name. For example: x, y, \_ = get_data() (x and y are used but since we don't care about third variable, we "threw it away").   
   
## Explain what is GIL   
   
    Python Global Interpreter Lock (GIL) is a type of process lock which is used by python whenever it deals with processes. Generally, Python only uses only one thread to execute the set of written statements. This means that in python only one thread will be executed at a time   
   
## What is Lambda? How is it used?   
   
A <code>lambda</code> expression is an 'anonymous' function, the difference from a normal defined function using the keyword `def`` is the syntax and usage.   
   
The syntax is:   
   
`lambda[parameters]: [expresion]`   
   
**Examples:**   
   
   
- A lambda function add 10 with any argument passed.   
   
```py
x = lambda a: a + 10
print(x(10))
```
   
   
   
- An addition function   
   
```py
addition = lambda x, y: x + y
print(addition(10, 20))
```
   
   
   
- Squaring function   
   
```py
square = lambda x : x ** 2
print(square(5))
```
   
   
Generally it is considered a bad practice under PEP 8 to assign a lambda expresion, they are meant to be used as parameters and inside of other defined functions.   
   
#### Properties   
   
## Are there private variables in Python? How would you make an attribute of a class, private?   
   
## Explain the following:   
   
   
- getter   
- setter   
- deleter   
   
## Explain what is @property   
   
## How do you swap values between two variables?   
   
```
x, y = y, x
```
   
   
## Explain the following object's magic variables:   
   
   
- **dict**   
   
## Write a function to return the sum of one or more numbers. The user will decide how many numbers to use   
   
First you ask the user for the amount of numbers that will be use. Use a while loop that runs until amount_of_numbers becomes 0 through subtracting amount_of_numbers by one each loop. In the while loop you want ask the user for a number which will be added a variable each time the loop runs.   
   
```
def return_sum():
	amount_of_numbers = int(input("How many numbers? "))
	total_sum = 0
	while amount_of_numbers != 0:
		num = int(input("Input a number. "))
		total_sum += num
		amount_of_numbers -= 1
	return total_sum

```
   
   
## Print the average of [2, 5, 6]. It should be rounded to 3 decimal places   
   
```
li = [2, 5, 6]
print("{0:.3f}".format(sum(li)/len(li)))
```
   
   
#### Python - Lists   
   
## What is a tuple in Python? What is it used for?   
   
A tuple is a built-in data type in Python. It's used for storing multiple items in a single variable.   
   
## List, like a tuple, is also used for storing multiple items. What is then, the difference between a tuple and a list?   
   
List, as opposed to a tuple, is a mutable data type. It means we can modify it and at items to it.   
   
## How to add the number 2 to the list <code>x = [1, 2, 3]</code>   
   
`x.append(2)`   
   
## How to get the last element of a list?   
   
`some_list[-1]`   
   
## How to add the items of [1, 2, 3] to the list [4, 5, 6]?   
   
x = [4, 5, 6]   
x.extend([1, 2, 3])   
   
Don't use `append` unless you would like the list as one item.   
   
## How to remove the first 3 items from a list?   
   
`my_list[0:3] = []`   
   
## How to insert an item to the beginning of a list? What about two items?   
   
   
- One item:   
   
```
numbers = [1, 2, 3, 4, 5]
numbers.insert(0, 0)
print(numbers)
```
   
   
   
- Multiple items or list:   
   
```
numbers_1 = [2, 3, 4, 5]
numbers_2 = [0, 1]
numbers_1 = numbers_2 + numbers_1
print(numbers_1)
```
   
   
## How to sort list by the length of items?   
   
```
sorted_li = sorted(li, key=len)
```
   
   
Or without creating a new list:   
   
```
li.sort(key=len)
```
   
   
## Do you know what is the difference between list.sort() and sorted(list)?   
   
   
- sorted(list) will return a new list (original list doesn't change)   
- list.sort() will return None but the list is change in-place   
   
   
- sorted() works on any iterable (Dictionaries, Strings, ...)   
- list.sort() is faster than sorted(list) in case of Lists   
   
## Convert every string to an integer: <code>[['1', '2', '3'], ['4', '5', '6']]</code>   
   
```
nested_li = [['1', '2', '3'], ['4', '5', '6']]
[[int(x) for x in li] for li in nested_li]
```
   
   
## How to merge two sorted lists into one sorted list?   
   
```
sorted(li1 + li2)
```
   
   
Another way:   
   
```
i, j = 0
merged_li = []

while i < len(li1) and j < len(li2):
    if li1[i] < li2[j]:
        merged_li.append(li1[i])
        i += 1
    else:
        merged_li.append(li2[j])
        j += 1

merged_li = merged_li + merged_li[i:] + merged_li[j:]
```
   
   
## How to check if all the elements in a given lists are unique? so [1, 2, 3] is unique but [1, 1, 2, 3] is not unique because 1 exists twice   
   
</b>   
   
There are many ways of solving this problem:<br>   
<code># Note: :list and -> bool are just python typings, they are not needed for the correct execution of the algorithm. </code>   
   
Taking advantage of sets and len:   
   
```
def is_unique(l:list) -> bool:
    return len(set(l)) == len(l)
```
   
   
This one is can be seen used in other programming languages.   
   
```
def is_unique2(l:list) -> bool:
    seen = []

    for i in l:
        if i in seen:
            return False
        seen.append(i)
    return True
```
   
   
Here we just count and make sure every element is just repeated once.   
   
```
def is_unique3(l:list) -> bool:
    for i in l:
        if l.count(i) > 1:
            return False
    return True
```
   
   
This one might look more convulated but hey, one liners.   
   
```
def is_unique4(l:list) -> bool:
    return all(map(lambda x: l.count(x) < 2, l))
```
   
   
</details>   
   
## You have the following function   
   
```
def my_func(li = []):
    li.append("hmm")
    print(li)
```
   
   
If we call it 3 times, what would be the result each call?   
   
```
['hmm']
['hmm', 'hmm']
['hmm', 'hmm', 'hmm']
```
   
   
## How to iterate over a list?   
   
```
for item in some_list:
    print(item)
```
   
   
## How to iterate over a list with indexes?   
   
```
for i, item in enumerate(some_list):
    print(i)
```
   
   
## How to start list iteration from 2nd index?   
   
Using range like this   
   
```
for i in range(1, len(some_list)):
    some_list[i]
```
   
   
Another way is using slicing   
   
```
for i in some_list[1:]:
```
   
   
## How to iterate over a list in reverse order?   
   
Method 1   
   
```
for i in reversed(li):
    ...
```
   
   
Method 2   
   
```
n = len(li) - 1
while n > 0:
    ...
    n -= 1
```
   
   
## Sort a list of lists by the second item of each nested list   
   
```
li = [[1, 4], [2, 1], [3, 9], [4, 2], [4, 5]]

sorted(li, key=lambda l: l[1])
```
   
   
or   
   
```
li.sort(key=lambda l: l[1)
```
   
   
## Combine [1, 2, 3] and ['x', 'y', 'z'] so the result is [(1, 'x'), (2, 'y'), (3, 'z')]   
   
```
nums = [1, 2, 3]
letters = ['x', 'y', 'z']

list(zip(nums, letters))
```
   
   
## What is List Comprehension? Is it better than a typical loop? Why? Can you demonstrate how to use it?   
   
From [Docs](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions): "List comprehensions provide a concise way to create lists. Common applications are to make new lists where each element is the result of some operations applied to each member of another sequence or iterable, or to create a subsequence of those elements that satisfy a certain condition.".   
   
It's better because they're compact, faster and have better readability.   
   
   
- For loop:   
   
```
number_lists = [[1, 7, 3, 1], [13, 93, 23, 12], [123, 423, 456, 653, 124]]
odd_numbers = []
for number_list in number_lists:
    for number in number_list:
        if number % 2 == 0:
            odd_numbers.append(number)
print(odd_numbers)
```
   
   
   
- List comprehesion:   
   
```
number_lists = [[1, 7, 3, 1], [13, 93, 23, 12], [123, 423, 456, 653, 124]]
odd_numbers = [number for number_list in number_lists for number in number_list if number % 2 == 0]
print(odd_numbers)
```
   
   
## You have the following list: <code>[{'name': 'Mario', 'food': ['mushrooms', 'goombas']}, {'name': 'Luigi', 'food': ['mushrooms', 'turtles']}]</code>   
   
Extract all type of foods. Final output should be: {'mushrooms', 'goombas', 'turtles'}   
   
```
brothers_menu =  \
[{'name': 'Mario', 'food': ['mushrooms', 'goombas']}, {'name': 'Luigi', 'food': ['mushrooms', 'turtles']}]

# "Classic" Way
def get_food(brothers_menu) -> set:
    temp = []

    for brother in brothers_menu:
        for food in brother['food']:
            temp.append(food)

    return set(temp)

# One liner way (Using list comprehension)
set([food for bro in x for food in bro['food']])
```
   
   
#### Python - Dictionaries   
   
## How to create a dictionary?   
   
my_dict = dict(x=1, y=2)   
OR   
my_dict = {'x': 1, 'y': 2}   
OR   
my_dict = dict([('x', 1), ('y', 2)])   
   
## How to remove a key from a dictionary?   
   
del my_dict['some_key']   
you can also use `my_dict.pop('some_key')` which returns the value of the key.   
   
## How to sort a dictionary by values?   
   
```
{k: v for k, v in sorted(x.items(), key=lambda item: item[1])}
```
   
   
## How to sort a dictionary by keys?   
   
```
dict(sorted(some_dictionary.items()))
```
   
   
## How to merge two dictionaries?   
   
```
some_dict1.update(some_dict2)
```
   
   
## Convert the string "a.b.c" to the dictionary <code>{'a': {'b': {'c': 1}}}</code>   
   
```
output = {}
string = "a.b.c"
path = string.split('.')
target = reduce(lambda d, k: d.setdefault(k, {}), path[:-1], output)
target[path[-1]] = 1
print(output)
```
   
   
##### Common Algorithms Implementation   
   
## Can you implement "binary search" in Python?   
   
[Solution](coding/python/binary_search.py)   
   
#### Python Files   
   
## How to write to a file?   
   
```
with open('file.txt', 'w') as file:
    file.write("My insightful comment")
```
   
   
## Sum all the integers in a given file   
   
## Print a random line of a given file   
   
## Print every 3rd line of a given file   
   
## Print the number of lines in a given file   
   
## Print the number of of words in a given file   
   
## Can you write a function which will print all the file in a given directory? including sub-directories   
   
## Write a dictionary (variable) to a file   
   
```
import json

with open('file.json', 'w') as f:
    f.write(json.dumps(dict_var))
```
   
   
## How to print current working directory?   
   
    import os   
   
    print(os.getcwd())   
   
## Given the path <code>/dir1/dir2/file1</code> print the file name (file1)   
   
    import os   
   
    print(os.path.basename('/dir1/dir2/file1'))   
   
# Another way   
    print(os.path.split('/dir1/dir2/file1')[1])   
   
## Given the path <code>/dir1/dir2/file1</code>   
   
1. Print the path without the file name (/dir1/dir2)   
2. Print the name of the directory where the file resides (dir2)   
   
   import os   
   
## Part 1.   
   
# os.path.dirname gives path removing the end component   
   
   dirpath = os.path.dirname('/dir1/dir2/file1')   
   print(dirpath)   
   
## Part 2.   
   
   print(os.path.basename(dirpath))   
   
## How do you execute shell commands using Python?   
   
## How do you join path components? for example <code>/home</code> and <code>luig</code> will result in <code>/home/luigi</code>   
   
## How do you remove non-empty directory?   
   
## How do you perform regular expressions related operations in Python? (match patterns, substitute strings, etc.)   
   
Using the re module   
   
## How to find all the IP addresses in a variable? How to find them in a file?   
   
## Find the first repeated character in a string   
   
While you iterate through the characters, store them in a dictionary and check for every character whether it's already in the dictionary.   
   
```
def firstRepeatedCharacter(str):
    chars = {}
    for ch in str:
        if ch in chars:
            return ch
        else:
            chars[ch] = 0
```
   
   
## How to extract the unique characters from a string? for example given the input "itssssssameeeemarioooooo" the output will be "mrtisaoe"   
   
```
x = "itssssssameeeemarioooooo"
y = ''.join(set(x))
```
   
   
## Find all the permutations of a given string   
   
```
def permute_string(string):

    if len(string) == 1:
        return [string]

    permutations = []
    for i in range(len(string)):
        swaps = permute_string(string[:i] + string[(i+1):])
        for swap in swaps:
            permutations.append(string[i] + swap)

    return permutations

print(permute_string("abc"))
```
   
   
Short way (but probably not acceptable in interviews):   
   
```
from itertools import permutations

[''.join(p) for p in permutations("abc")]
```
   
   
Detailed answer can be found here: [http://codingshell.com/python-all-string-permutations](http://codingshell.com/python-all-string-permutations)   
   
## How to check if a string contains a sub string?   
   
## Find the frequency of each character in string   
   
## Count the number of spaces in a string   
   
You can use the "count" method like this:   
   
```python

ImAString.count(" ")

```
   
   
## Given a string, find the N most repeated words   
   
## Given the string (which represents a matrix) "1 2 3\n4 5 6\n7 8 9" create rows and colums variables (should contain integers, not strings)   
   
## What is the result of each of the following?   
   
```
>> ', '.join(["One", "Two", "Three"])
>> " ".join("welladsadgadoneadsadga".split("adsadga")[:2])
>> "".join(["c", "t", "o", "a", "o", "q", "l"])[0::2]
```
   
   
```
>>> 'One, Two, Three'
>>> 'well done'
>>> 'cool'
```
   
   
## If <code>x = "pizza"</code>, what would be the result of <code>x[::-1]</code>?   
   
It will reverse the string, so x would be equal to `azzip`.   
   
## Reverse each word in a string (while keeping the order)   
   
## What is the output of the following code: <code>"".join(["a", "h", "m", "a", "h", "a", "n", "q", "r", "l", "o", "i", "f", "o", "o"])[2::3]</code>   
   
mario   
   
## What is an iterator?   
   
## Explain data serialization and how do you perform it with Python   
   
## How do you handle argument parsing in Python?   
   
## What is a generator? Why using generators?   
   
## What would be the output of the following block?   
   
```
for i in range(3, 3):
   print(i)
```
   
   
No output :)   
   
## What is <code>yeild</code>? When would you use it?   
   
## Explain the following types of methods and how to use them:   
   
   
- Static method   
- Class method   
- instance method   
   
## How to reverse a list?   
   
## How to combine list of strings into one string with spaces between the strings   
   
## You have the following list of nested lists: <code>[['Mario', 90], ['Geralt', 82], ['Gordon', 88]]</code> How to sort the list by the numbers in the nested lists?</code>   
   
One way is:   
   
the_list.sort(key=lambda x: x[1])   
   
## Explain the following:   
   
   
- zip()   
- map()   
- filter()   
   
23For the following slicing exercises, assume you have the following list: `my_list = [8, 2, 1, 10, 5, 4, 3, 9]`   
   
## What is the result of `my_list[0:4]`?   
   
## What is the result of `my_list[5:6]`?   
   
## What is the result of `my_list[5:5]`?   
   
## What is the result of `my_list[::-1]`?   
   
## What is the result of `my_list[::3]`?   
   
## What is the result of `my_list[2:]`?   
   
## What is the result of `my_list[:3]`?   
   
## How do you debug Python code?   
   
pdb :D   
   
## How to check how much time it took to execute a certain script or block of code?   
   
## What empty <code>return</code> returns?   
   
</b>   
   
Short answer is: It returns a None object.   
   
We could go a bit deeper and explain the difference between   
   
```
def a ():
    return

>>> None
```
   
   
And   
   
```
def a ():
    pass

>>> None
```
   
   
Or we could be asked this as a following question, since they both give the same result.   
   
We could use the dis module to see what's going on:   
   
```
  2           0 LOAD_CONST               0 (<code object a at 0x0000029C4D3C2DB0, file "<dis>", line 2>)
              2 LOAD_CONST               1 ('a')
              4 MAKE_FUNCTION            0
              6 STORE_NAME               0 (a)

  5           8 LOAD_CONST               2 (<code object b at 0x0000029C4D3C2ED0, file "<dis>", line 5>)
             10 LOAD_CONST               3 ('b')
             12 MAKE_FUNCTION            0
             14 STORE_NAME               1 (b)
             16 LOAD_CONST               4 (None)
             18 RETURN_VALUE

Disassembly of <code object a at 0x0000029C4D3C2DB0, file "<dis>", line 2>:
  3           0 LOAD_CONST               0 (None)
              2 RETURN_VALUE

Disassembly of <code object b at 0x0000029C4D3C2ED0, file "<dis>", line 5>:
  6           0 LOAD_CONST               0 (None)
              2 RETURN_VALUE
```
   
   
An empty <code> return</code> is exactly the same as <code>return None</code> and functions without any explicit return   
will always return None regardless of the operations, therefore   
   
```
def sum(a, b):
    global c
    c = a + b

>>> None
```
   
   
## How to improve the following block of code?   
   
```
li = []
for i in range(1, 10):
    li.append(i)
```
   
   
```
[i for i in range(1, 10)]
```
   
   
## Given the following function   
   
```
def is_int(num):
    if isinstance(num, int):
        print('Yes')
    else:
        print('No')
```
   
   
What would be the result of is_int(2) and is_int(False)?   
   
## Can you implement a linked list in Python?   
   
The reason we need to implement in the first place, it's because a linked list isn't part of Python standard library.<br>   
To implement a linked list, we have to implement two structures: The linked list itself and a node which is used by the linked list.   
   
Let's start with a node. A node has some value (the data it holds) and a pointer to the next node   
   
```
class Node(object):
    def __init__(self, data):
        self.data = data
        self.next = None
```
   
   
Now the linked list. An empty linked list has nothing but an empty head.   
   
```
class LinkedList(object):
    def __init__(self):
        self.head = None
```
   
   
Now we can start using the linked list   
   
```
ll = Linkedlist()
ll.head = Node(1)
ll.head.next = Node(2)
ll.head.next.next = Node(3)
```
   
   
What we have is:   
   
   
---   
   
| 1 | -> | 2 | -> | 3 |   
   
   
---   
   
Usually, more methods are implemented, like a push_head() method where you insert a node at the beginning of the linked list   
   
```
def push_head(self, value):
    new_node = Node(value)
    new_node.next = self.head
    self.head = new_node
```
   
   
## Add a method to the Linked List class to traverse (print every node's data) the linked list   
   
def print_list(self):   
node = self.head   
while(node):   
print(node.data)   
node = node.next   
   
## Write a method to that will return a boolean based on whether there is a loop in a linked list or not   
   
Let's use the Floyd's Cycle-Finding algorithm:   
   
```
def loop_exists(self):
    one_step_p = self.head
    two_steps_p = self.head
    while(one_step_p and two_steps_p and two_steps_p.next):
        one_step_p = self.head.next
        two_step_p = self.head.next.next
        if (one_step_p == two_steps_p):
            return True
    return False
```
   
   
## Implement Stack in Python   
   
## What is your experience with writing tests in Python?   
   
## What is PEP8? Give an example of 3 style guidelines   
   
PEP8 is a list of coding conventions and style guidelines for Python   
   
5 style guidelines:   
   
    1. Limit all lines to a maximum of 79 characters.   
    2. Surround top-level function and class definitions with two blank lines.   
    3. Use commas when making a tuple of one element   
    4. Use spaces (and not tabs) for indentation   
    5. Use 4 spaces per indentation level   
   
## How to test if an exception was raised?   
   
## What <code>assert</code> does in Python?   
   
## Explain mocks   
   
## How do you measure execution time of small code snippets?   
   
## Why one shouldn't use <code>assert</code> in non-test/production code?   
   
## Can you describe what is Django/Flask and how you have used it? Why Flask and not Django? (or vice versa)   
   
## What is a route?   
   
As every web framework, Flask provides a route functionality that lets you serve a content of a given URL.   
   
There are multiple ways to map a URL with a function in Python.   
   
   
- Decorator: you can use python decorators. In this case we're using `app`. This `app` decorator is the instance of the `Flask` class. And route it's a method of this class.   
   
```
@app.route('/')
def home():
  return 'main website'
```
   
   
   
- `add_url_rule` method: This is a method of the Flask class. We can also use it for map the URL with a function.   
   
```
def home():
  return 'main website'

app.add_url_rule('/', view_func=home)
```
   
   
## What is a blueprint in Flask?   
   
## What is a template?   
   
## Given <code>x = [1, 2, 3]</code>, what is the result of list(zip(x))?   
   
```
[(1,), (2,), (3,)]
```
   
   
## What is the result of each of the following:   
   
```
list(zip(range(5), range(50), range(50)))
list(zip(range(5), range(50), range(-2)))
```
   
   
```
[(0, 0, 0), (1, 1, 1), (2, 2, 2), (3, 3, 3), (4, 4, 4)]
[]
```
   
   
## Explain Descriptors   
   
Read about descriptors [here](https://docs.python.org/3/howto/descriptor.html)   
   
## What would be the result of running <code>a.num2</code> assuming the following code   
   
```
class B:
    def __get__(self, obj, objtype=None):
        reuturn 10

class A:
    num1 = 2
    num2 = Five()
```
   
   
10   
   
## What would be the result of running <code>some_car = Car("Red", 4)</code> assuming the following code   
   
```
class Print:

    def __get__(self, obj, objtype=None):
        value = obj._color
        print("Color was set to {}".format(valie))
        return value

    def __set__(self, obj, value):
        print("The color of the car is {}".format(value))
        obj._color = value

class Car:

    color = Print()

    def __ini__(self, color, age):
        self.color = color
        self.age = age
```
   
   
An instance of Car class will be created and the following will be printed: "The color of the car is Red"   
   
## How can you spawn multiple processes with Python?   
   
## Implement simple calculator for two numbers   
   
```
def add(num1, num2):
    return num1 + num2


def sub(num1, num2):
    return num1 - num2


def mul(num1, num2):
    return num1*num2


def div(num1, num2):
    return num1 / num2

operators = {
    '+': add,
    '-': sub,
    '*': mul,
    '/': div
}

if __name__ == '__main__':
    operator = str(input("Operator: "))
    num1 = int(input("1st number: "))
    num2 = int(input("2nd number: "))
    print(operators[operator](num1, num2))
```
   
   
## What data types are you familiar with that are not Python built-in types but still provided by modules which are part of the standard library?   
   
This is a good reference [https://docs.python.org/3/library/datatypes.html](https://docs.python.org/3/library/datatypes.html)   
   
## Explain what is a decorator   
   
In python, everything is an object, even functions themselves. Therefore you could pass functions as arguments   
for another function eg;   
   
```
def wee(word):
    return word

def oh(f):
    return f + "Ohh"

>>> oh(wee("Wee"))
<<< Wee Ohh
```
   
   
This allows us to control the before execution of any given function and if we added another function as wrapper,   
(a function receiving another function that receives a function as parameter) we could also control the after execution.   
   
Sometimes we want to control the before-after execution of many functions and it would get tedious to write   
   
<code> f = function(function_1())</code>   
<code> f = function(function_1(function_2(\*args)))</code>   
   
every time, that's what decorators do, they introduce syntax to write all of this on the go, using the keyword '@'.   
</b>   
   
</details>   
   
## Can you show how to write and use decorators?   
   
<code>   
These two decorators (ntimes and timer) are usually used to display decorators functionalities, you can find them in lots of   
tutorials/reviews. I first saw these examples two years ago in pyData 2017. [https://www.youtube.com/watch?v=7lmCu8wz8ro&t=3731s</code>](https://www.youtube.com/watch?v=7lmCu8wz8ro&t=3731s</code>)   
   
```
Simple decorator:

def deco(f):
    print(f"Hi I am the {f.__name__}() function!")
    return f

@deco
def hello_world():
    return "Hi, I'm in!"

a = hello_world()
print(a)

>>> Hi I am the hello_world() function!
    Hi, I'm in!
```
   
   
This is the simplest decorator version, it basically saves us from writting <code>a = deco(hello_world())</code>.   
But at this point we can only control the before execution, let's take on the after:   
   
```
def deco(f):
    def wrapper(*args, **kwargs):
        print("Rick Sanchez!")
        func = f(*args, **kwargs)
        print("I'm in!")
        return func
    return wrapper

@deco
def f(word):
    print(word)

a = f("************")
>>> Rick Sanchez!
    ************
    I'm in!
```
   
   
deco receives a function -> f   
wrapper receives the arguments -> \*args, \*\*kwargs   
   
wrapper returns the function plus the arguments -> f(\*args, \*\*kwargs)   
deco returns wrapper.   
   
As you can see we conveniently do things before and after the execution of a given function.   
   
For example, we could write a decorator that calculates the execution time of a function.   
   
```
import time
def deco(f):
    def wrapper(*args, **kwargs):
        before = time.time()
        func = f(*args, **kwargs)
        after = time.time()
        print(after-before)
        return func
    return wrapper

@deco
def f():
    time.sleep(2)
    print("************")

a = f()
>>> 2.0008859634399414
```
   
   
Or create a decorator that executes a function n times.   
   
```
def n_times(n):
    def wrapper(f):
        def inner(*args, **kwargs):
            for _ in range(n):
                func = f(*args, **kwargs)
            return func
        return inner
    return wrapper

@n_times(4)
def f():
    print("************")

a = f()

>>>************
   ************
   ************
   ************
```
   
   
## Write a decorator that calculates the execution time of a function   
   
## Write a script which will determine if a given host is accessible on a given port   
   
## Are you familiar with Dataclasses? Can you explain what are they used for?   
   
## You wrote a class to represent a car. How would you compare two cars instances if two cars are equal if they have the same model and color?   
   
```
class Car:
    def __init__(self, model, color):
        self.model = model
        self.color = color

    def __eq__(self, other):
        if not isinstance(other, Car):
            return NotImplemented
        return self.model == other.model and self.color == other.color

>> a = Car('model_1', 'red')
>> b = Car('model_2', 'green')
>> c = Car('model_1', 'red')
>> a == b
False
>> a == c
True
```
   
   
## Explain Context Manager   
   
## Tell me everything you know about concurrency in Python   
   
## Explain the Buffer Protocol   
   
## Do you have experience with web scraping? Can you describe what have you used and for what?   
   
## Can you implement Linux's <code>tail</code> command in Python? Bonus: implement <code>head</code> as well   
   
## You have created a web page where a user can upload a document. But the function which reads the uploaded files, runs for a long time, based on the document size and user has to wait for the read operation to complete before he/she can continue using the web site. How can you overcome this?   
   
## How yield works exactly?