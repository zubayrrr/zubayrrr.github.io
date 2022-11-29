---
created: 20211010125448064
desc: ''
id: 1nxa1evrapl0z06rszqums9
title: Session Layer - OSI
updated: 1656561544225
---
   
# Layer 5 – Session Layer   
   
Think of a session as a conversation that must be kept separate from others to prevent intermingling of the data.   
   
This layer permits the users of different platforms to set up an active communication session between themselves.   
   
The main function of this layer is to provide sync in the dialogue between the two distinctive applications. The synchronization is necessary for efficient delivery of data without any loss at the receiver end.   
   
**Example.**   
   
Assume that a sender is sending a big data file of more than 2000 pages. This layer will add some checkpoints while sending the big data file. After sending a small sequence of 40 pages, it ensures the sequence & successful acknowledgment of data.   
   
If verification is OK, it will keep repeating it further till the end otherwise it will re-synchronize and re-transmit.   
   
This will help in keeping the data safe and the whole data host will never completely get lost if some crash happens. Also, token management, will not allow two networks of heavy data and of the same type to transmit at the same time.   
   
### Setting up a Session   
   
   
- Check user credentials   
- Assign numbers to session to identify them   
- Negotiate services needed for session   
- Negotiate who begins sending data   
   
   
---   
   
### Maintaining Session   
   
   
- Transfer the data   
- Reestablish a disconnected session   
- Acknowledging receipt of data   
   
   
---   
   
### Tearing Down a Session   
   
   
- Due to mutual agreement   
  - After the transfer is done   
- Due to other party disconnecting   
   
   
---   
   
### Layer 5 Examples   
   
   
- [H323](../devlog/H323.md)   
  - Used to setup, maintain, and tear down a voice/video connection.   
- [NetBIOS](../devlog/netbios.md)   
  - Used by computers to share files over a network.