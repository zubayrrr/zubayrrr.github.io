---
created: '2021-10-09T00:00:00.000Z'
desc: ''
id: yjeoqhn1zs6blkof49hvacr
title: Physical Layer - OSI
updated: 1656501900042
---
   
# Layer 1 – Physical layer   
   
This where the transmission of bits across the network occurs and is focused on the physical and electrical characteristics of the network.   
   
There is where we decide if we're using an [Ethernet](../devlog/ethernet.md) network or if we're using [Fiber Optic](../devlog/fiber%20optic.md), or Copper cables.   
   
No matter what method we're using to transmit our data, it will always be in the form of binary [bit](../devlog/bit.md)s   
   
Binary [bit](../devlog/bit.md)s are series of 1s and 0s.   
   
Each media has different ways of representing these [bit](../devlog/bit.md)s   
   
For example, if we're using a Copper wire such as in a [Cat5](/not_created.md) or [Cat6](/not_created.md) network, you'll find that the voltage of the wire will be zero for a 0 [bit](../devlog/bit.md) and to represent a 1, you might use a +5 or -5 voltage on the Copper wire.   
   
**Transition Modulation** is what dictates the change is (or how it should be interpreted), If it changed during the clock cycle, then a 1 is represented (otherwise it is a 0).   
   
In case of a [Fiber Optic](../devlog/fiber%20optic.md) cable, we'll be using light instead of voltages; when we want a 1, we turn the light on. when we want to represent a 0, we turn the light off.   
   
   
---   
   
Once we have the data from the [Media](../topics/media.md), we'll have [Connector Types](../devlog/connector%20types.md) on the end of the cables that go inside our devices. These connectors are wired based on a standard.   
   
   
- TIA/EIA-568-B   
  - [RJ-45](../devlog/rj-45.md) cables and ports   
- T-568A and T-568B   
  - Crossover cables   
- [Straight-Through Patch Cable](../devlog/straight-through%20patch%20cable.md) typically uses T-568B on both ends, but could also use T-568A.   
- See: [Pinouts](../devlog/pinouts.md)   
   
### Topology of the network at the Physical Layer   
   
   
- Layer 1 devices view networks from a physical topology perspective, as discussed in [Wired Network Topology](../devlog/wired%20network%20topology.md) & [Wireless Network Topology](../devlog/wireless%20network%20topology.md).   
   
   
---   
   
### Synchronizing communication at Physical Layer   
   
How do we know that the receiving end is ready to accept the [bit](../devlog/bit.md)s that we're ready to send?   
   
   
- We can work this out either Asynchronously or Synchronously:   
   
#### Asynchronous   
   
   
- Uses "start bits" and "stop bits" to indicate when transmissions occur from sender to receiver.   
   
#### Synchronous   
   
   
- Uses a reference block to coordinate the transmissions by both sender and receiver. Happens in Real-time. Uses a time source, transmits data on the cadence of the time.   
   
   
---   
   
### How is the bandwidth utilized?   
   
There are again two ways, Broadband and Baseband.   
   
#### Broadband   
   
   
- Divides bandwidth into separate channels. (e.g. Cable TV)   
   
#### Baseband   
   
   
- Uses all available frequencies on a medium (cable) to transmit data and uses a reference clock to coordinate the transmissions by both sender and receiver. (e.g. Telephone, Home [Ethernet](../devlog/ethernet.md))   
   
   
---   
   
### If we're using a single Baseband using all of the bandwidth how can we get more out of a limited network?   
   
   
- Time-Division Multiplexing (TDM)   
  - Each session takes a turn, using time slots, to share the medium between all users.   
- Statistical Time-Division Multiplexing (StatTDM)   
  - More efficient version of TDM since it dynamically allocates time slots on an as-needed basis instead of statically assigning.   
- Frequency-Division Multiplexing (FDM)   
  - Medium is divided into various channels based on frequencies and each session is transmitted over a different channel.   
   
   
---   
   
### Media at Layer 1 (Layer 1 Examples)   
   
Devices that give physical response, hence a physical layer device.   
   
   
- Cables   
  - [Ethernet](../devlog/ethernet.md)   
  - [Fiber Optic](../devlog/fiber%20optic.md)   
- Radio Frequencies   
  - [Wi-Fi](../devlog/wi-fi.md)   
  - [Bluetooth](../devlog/Bluetooth.md)   
  - [NFC](../devlog/nfc.md)   
- Infrastructure Devices   
  - [Hub](../devlog/hub.md)s   
  - Wireless Access Points   
  - [Media Converters](../devlog/media%20converters.md)