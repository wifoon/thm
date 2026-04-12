
The OSI (Open Systems Interconnection) model is a conceptual model that describes how communications should occur in a computer network.

![367](../attachments/Pasted%20image%2020260412223916.png)

#### Layer 1: Physical Layer

The physical layer, also referred to as layer 1, deals with the physical connection between devices.

#### Layer 2: Data Link Layer

The data link layer, layer 2, represents the protocol that enables data transfer between nodes on the same network segment. The data link layer describes an agreement between the different systems on the same network segment on how to communicate.

#### Layer 3: Network Layer

The network layer, layer 3, is concerned with sending data between different networks. It handles logical addressing and routing, i.e., finding a path to transfer the network packets between the diverse networks.

Examples of the network layer include Internet Protocol (IP), Internet Control Message Protocol (ICMP), and Virtual Private Network (VPN) protocols such as IPSec and SSL/TLS VPN.
#### Layer 4: Transport Layer

Layer 4, the transport layer, enables end-to-end communication between running applications on different hosts. Web browser is connected to the another web server over the transport layer, which can support various functions like flow control, segmentation, and error correction.

Examples of layer 4 are Transmission Control Protocol (TCP) and User Datagram Protocol (UDP).

#### Layer 5: Session Layer

The session layer is responsible for establishing, maintaining, and synchronising communication between applications running on different hosts. Establishing a session means initiating communication between applications and negotiating the necessary parameters for the session. Data synchronisation ensures that data is transmitted in the correct order and provides mechanisms for recovery in case of transmission failures.

Examples of the session layer are Network File System (NFS) and Remote Procedure Call (RPC).

#### Layer 6: Presentation Layer

The presentation layer ensures the data is delivered in a form the application layer can understand. Layer 6 handles data encoding, compression, and encryption. An example of encoding is character encoding, such as ASCII or Unicode.

