# NetPractice
An informative document about the workings of basic networking concepts like TCP/IP addressing and subnet masks.

## TCP/IP addressing

- A scheme that allows users and applications to identify a specific network or host to send signals between.
- An Internet address allows data to be routed to chosen destinations.
  - TCP/IP sets standards for assigning addresses to networks, subnetworks, hosts and sockets.
  - This includes addresses that are unique for broadcasts and local loopbacks

- Internet addresses use a network address and a host/local address.
  - Both let a sender specify both the network and the specific host on the network.
  - An official and unique network address is used for each network when it connects to Internet networks.
  - If a network only connects locally and not to Internet networks, it can have any network address this is convenient for local use.

- Internet addressing schemes use Internet Protocol (IP) addresses with 2 special subsets - broadcast addresses and loopback addresses.
- IP uses a 32-bit, 2 part address field.
- Subnet addressing allows for autonomous systems with multiple networks to share the same Internet address.
- Broadcast addresses - can be used to send data to all hosts on a local network/directly connected networks. Aka broadcast messages.
- Local loopback address: 127.0.0.1 (unique specified network for loopbacks)

## Internet addresses

- 32-bit
  - Four octets:
      01111101 00001101 01001001 00001111:
      125 13 73 15
- 2 parts to an Internet address:
  - Network address part
  - Host address part
  - Lets remote host to specify remote network and host on the remote network for sending data.
  - Host number of 0 refers to the network itself.

- TCP/IP has 3 classes
  - Networks are assigned address class based on size of network.

  - Class A
    - 8-bit network address & 24-bit local/host address.
  - Class B
    - 16-bit network address & 16-bit local/host address.
  - Class C
    - 24-bit network address & 8-bit local/host address.
    - 0 as host portion TCP/IP sends a wildcard address to the network. (192.9.200.0)

### Class A

- First bit indicates network class.
- 7 bits for network address. Highest 7 bit representation is 128.
  - 128 possible Class A networks.
  - Network address 127 is for local loopback.
  - Network address with all ones is for a broadcast address.

- 126 Class A network addresses exist
- 16,777,7216 possible local host addresses.

- Highest order bit is 0.

| Network Address (8 bits) | Local Host Address (24 bits) |
| ------------------------ | ---------------------------- |
| 01111101 | 00001101 01001001 00001111 |
| 125 | 13 73 15 |

### Class B

- First 2 bits indicate network class.
- 14 bits for network address.
  - Between 128 to 191 networks in first octet.

- 16,384 network addresses.
- 65,536 local host addresses.

- Highest order bits are 1 and 0.

| Network Address (16 bits) | Local Host Address (16 bits) |
| ------------------------- | ---------------------------- |
| 10011101 00001101 | 01001001 00001111 |
| 157 13 | 73 15 |

### Class C

- First 3 bits indicate network class.
- 21 bits for network address.
  - Between 192 to 223 networks in first octet.

- 2,097,152 network addresses.
- 256 local host addresses.

- Highest order bits are 1, 1 and 0.

| Network Address (24 bits) | Local Host Address (8 bits) |
| ------------------------- | --------------------------- |
| 11011101 00001101 01001001 | 00001111 |
| 221 13 73 | 15 |

## Subnet addresses

- allows autonomous system of multiple networks to share same Internet address.
- can divide a network into multiple networks - subnets
- few Internet network address to interact externally while having multiple local/internal routes.
- IPs have 2 parts:
    - network address
    - local address
- Local address of Internet address is divided into a subnet number and a host number.
- Subnet addresses are created by dividing the local address into a number that ids the physical network/subnet & a number that ids the host.
    - Senders pass info to network address -> local system manages routing subnets
        and the messages being sent to them as well as their hosts.
- Assignment of subnet addresses and host addresses are flexible, minus a few
    restrictions:
    - network_address -> Internet address of the network
    - subnet_address -> constant width for a specified network
        - if set to 0, the network doesn't have subnets
            - addressing the network uses the Internet network address
        - identified through a bit mask (not adjacent in the address)
            - It is preferable to keep subnet bits consistent and addressed as the
                most significant bit of local_address
    - host_address -> minimum 1 bit wide

| Network Address (8 bits) | Local Host Address (24 bits) | - |
| ------------------------- | --------------------------- | --------------------------- |
| - | Subnet Address | Host Address |
| 01111101 | 00001101 0100 | 1001 00001111 |
| 125 | 13 4 | 9 15 |
| 125 | 13 73 15 | - |

- Subnet masks
    - When messages are sent, the system evaluates both the same network
        and local interfaces to determine the destination.
    - This comparison is done using the subnet mask
    - Set of 4 bytes.
        - Mostly higher bits (1's)
            - For the network and subnetwork address
        - Then low bits (0)'s
            - Bit positions of the host address

| Network Address (8 bits) | Local Host Address (24 bits) | - |
| ------------------------- | --------------------------- | --------------------------- |
| Network Address | Subnet Address | Host Address |
| 11111111 | 11111111 1111 | 0000 00000000 |
| 255 | 255 15 | 0 0 |
| 255 | 255 240 0 | - |

    - Subnet masks can be represented using a Full IP mask or with a CIDR
        (Classless Inter-Domain Routing)
    255.255.255.255 -> /32 (maximum IP mask & prefix)
    0.0.0.0 -> /0 (minimum IP mask & prefix)

| CIDR (prefix) | Subnet Mask | Bits | IP Addresses |
| ------------------------- | --------------------------- | ------------------------- | --------------------------- |
| /32 | 255.255.255.255 | 0 | 1 |
| /31 | 255.255.255.254 | 1 | 2 |
| /30 | 255.255.255.252 | 2 | 4 |
| /29 | 255.255.255.248 | 3 | 8 |
| /28 | 255.255.255.240 | 4 | 16 |
| /27 | 255.255.255.224 | 5 | 32 |
| /26 | 255.255.255.192 | 6 | 64 |
| /25 | 255.255.255.128 | 7 | 128 |
| /24 | 255.255.255.0 | 8 | 256 |
| /23 | 255.255.254.0 | 9 | 512 |
| /22 | 255.255.252.0 | 10 | 1 k |
| /21 | 255.255.248.0 | 11 | 2 k |
| /20 | 255.255.240.0 | 12 | 4 k |
| /19 | 255.255.224.0 | 13 | 8 k |
| /18 | 255.255.192.0 | 14 | 16 k |
| /17 | 255.255.128.0 | 15 | 32 k |
| /16 | 255.255.0.0 | 16 | 64 K |
| /15 | 255.254.0.0 | 17 | 128 K |
| /14 | 255.252.0.0 | 18 | 256 K |
| /13 | 255.248.0.0 | 19 | 512 K |
| /12 | 255.240.0.0 | 20 | 1 M |
| /11 | 255.224.0.0 | 21 | 2 M |
| /10 | 255.192.0.0 | 22 | 4 M |
| /9 | 255.128.0.0 | 23 | 8 M |
| /8 | 255.0.0.0 | 24 | 16 M |
| /7 | 254.0.0.0 | 25 | 32 M |
| /6 | 252.0.0.0 | 26 | 64 M |
| /5 | 248.0.0.0 | 27 | 128 M |
| /4 | 240.0.0.0 | 28 | 256 M |
| /3 | 224.0.0.0 | 29 | 512 M |
| /2 | 192.0.0.0 | 30 | 1024 M |
| /1 | 128.0.0.0 | 31 | 2048 M |
| /0 | 0.0.0.0 | 32 | 4096 M |

## TCP/IP routing

- Route defines a path for sending packets through the Internet network to an address on another network.
  - This only defines the path segment from one host to a gateway (gateways then continue communication).

- host route
  - Gateway that forwards packets to a specific host or another network.
- network route
  - Gateway that forwards packets to any hosts on a specific network.
- default route
  - Gateway for when host or network routes to a destination are not defined.
- loopback route
  - Default route for all packets sent to local network addresses.
    - IP is always 127.0.0.1
- broadcast route
  - Default for all broadcast packets.
    - 2 broadcast routes auto assign to each subnet on whcih the network has an IP.
      - To subnet address
      - To broadcast address of the subnet

## Routers VS Switches

### Switches

Primarily used for distributing packets to and from devices in the same network

- LANs - Local Area Networks
- No direct interface as it does not need to communicate with external networks.

### Routers

Responsible for connecting multiple networks.
- multiple LANs connected to each other, LAN(s) connected to the Internet, etc.
- each router has multiple interfaces, one for each network it is linked with.
- due to multiple netwroks being linked these interfaces should manage address
    range and subnet masks carefully to avoid overlap.

## OSI Layer

The OSI (Open Systems Interconnection) model is a conceptual framework made out of 7 layers.
- The applicable layers for this document/project are:
    - Layer 4: Transport layer
        - manage end-to-end communiation and flow control
        - TCP protocol
    - Layer 3: Network layer
        - manages addressing and routing packets across networks
        - IP protocol
