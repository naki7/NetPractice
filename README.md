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
<!-- finish -->

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


