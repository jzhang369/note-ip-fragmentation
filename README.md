# note-ip-fragmentation
some note on IP fragmentation

### Concepts

Maximum Transmission Unit (MTU): the largest number of bits a link can carray as one unit (e.g., a packet). 

Who can fragment an IP packet?

+ A router can fragment a packet into multiple fragments if the packet size exceeds the link's MTU. 

+ A sender can do it even if the packet size is smaller than the link's MTU. 

Who will de-fragmentation the fragments?

+ The end host. This is a classic case of the end-to-end design principle of the Internet.  

Why does not a router reassemble fragments?

+ Needs to be stateful: too expensive for core routers.

+ Fragments may traverse through different paths. 

IPv4's fragmentation fields

+ Identifier: an index value. 
+ Flags:

    - **R**eserved: ignore
    - **D**F: do not fragment
    - **M**F: more fragments coming (or I am not the last packet). 

Fragment withtout MF set indicates that this is the last fragment. 

### Security Concerns 

**Evading Network-Based Intrusion Detection Systems**

+ An attacker can split an IP packet that carries malicious content into a few fragments to disrupt the matching with a detection "signature". IDS can solve it by reassembling fragments, which is very expensive. 

+ An attacker can create overlapping fragments, for example [fragment1-offset-0: be], [fragment1-offset-2: good], and [fragment1-offset-2: evil]. Then the IDS cannot decide whether the receiver will see "be good" or "be evil" unless it knows how the receiver uses it. 

**State-Holding Attack**

An attacker can send some fragments without sending other fragments. The receiver will need to hold received fragments for a long time, aiming at waiting for other fragments.  

### IP Fragmentation Trace

One trace [1] is copied to the local directory for your reference. It contains a few fragmented IP packets. 

### References

[1] https://www.trueneutral.eu/files/20150120_wireshark-frags-1-1.pcapng