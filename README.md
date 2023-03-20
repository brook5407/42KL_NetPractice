<h1 align="center">
  📶NetPractice
</h1>

<p align="center">
	<b><i>This document is a System Administration related exercise</i></b><br>
</p>

<p align="center">
	<img alt="GitHub repo size" src="https://img.shields.io/github/repo-size/brook5407/42KL_NetPractice">
	<img alt="Lines of code" src="https://img.shields.io/tokei/lines/github/brook5407/42KL_NetPractice">
	<img alt="GitHub language count" src="https://img.shields.io/github/languages/count/brook5407/42KL_NetPractice">
	<img alt="GitHub top language" src="https://img.shields.io/github/languages/top/brook5407/42KL_NetPractice">
	<img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/brook5407/42KL_NetPractice">
</p>

<h3 align="center">
	<a href="#-about">About</a>
	<span> · </span>
  	<a href="#-content">Content</a>
	<span> · </span>
	<a href="#-level">Level</a>
</h3>

## 💡 About

> _This project is a general practical exercise to let you discover networking.._

## 🚀 Content

When you configure the TCP/IP protocol on a computer, the TCP/IP configuration settings require:
- [An IP address](#ip-addresses-networks-and-hosts)
- [A subnet mask](#subnet-mask)
- [A default gateway](#default-gateways)

IP addresses: Networks and hosts
---
An IP address is a 32-bit number. It uniquely identifies a host (computer or other device, such as a printer or router) on a TCP/IP network.

IP addresses are normally expressed in dotted-decimal format, with four numbers separated by periods, such as 172.16.254.1. To understand how subnet masks are used to distinguish between hosts, networks, and subnetworks, examine an IP address in binary notation.

For example, the dotted-decimal IP address `172.16.254.1` is (in binary notation) the 32-bit number`10101000110100101110000111001110`.

![white](https://user-images.githubusercontent.com/100013115/226153574-26ad0869-bcbe-4e4d-8ede-3704102f209a.png)
  
For a TCP/IP wide area network (WAN) to work efficiently as a collection of networks, the routers that pass packets of data between networks don't know the exact location of a host for which a packet of information is destined. Routers only know what network the host is a member of and use information stored in their route table to determine how to get the packet to the destination host's network. After the packet is delivered to the destination's network, the packet is delivered to the appropriate host.

For this process to work, an IP address has two parts. The first part of an IP address is used as a network address, the last part as a host address. If you take the example `192.168.123.132` and divide it into these two parts, you get `192.168.123`. Network `.132` Host or `192.168.123.0` - network address. `0.0.0.132` - host address.

IP-addresses for communication with itself:
```
From 127.0.0.1 to 127.255.255.254.
```

Private IP addresses (without access to the Internet):
```
From 10.0.0.0 to 10.255.255.255
From 172.16.0.0 to 172.31.255.255
From 192.168.0.0 to 192.168.255.255
```

Other IP addresses are public (with access to the Internet).

Subnet mask
---
The second item, which is required for TCP/IP to work, is the subnet mask. The subnet mask is used by the TCP/IP protocol to determine whether a host is on the local subnet or on a remote network.

In TCP/IP, the parts of the IP address that are used as the network and host addresses aren't fixed. Unless you have more information, the network and host addresses above can't be determined. This information is supplied in another 32-bit number called a subnet mask. The subnet mask is `255.255.255.0` in this example. It isn't obvious what this number means unless you know 255 in binary notation equals `11111111`. So, the subnet mask is `11111111.11111111.11111111.00000000`.

Lining up the IP address and the subnet mask together, the network, and host portions of the address can be separated:
```
11000000.10101000.01111011.10000100 - IP address (192.168.123.132)
11111111.11111111.11111111.00000000 - Subnet mask (255.255.255.0)
```

The first 24 bits (the number of ones in the subnet mask) are identified as the network address. The last 8 bits (the number of remaining zeros in the subnet mask) are identified as the host address. It gives you the following addresses:
```
11000000.10101000.01111011.00000000 - Network address (192.168.123.0)
00000000.00000000.00000000.10000100 - Host address (000.000.000.132)
```
So now you know, for this example using a `255.255.255.0` subnet mask, that the network ID is `192.168.123.0`, and the host address is `0.0.0.132`. When a packet arrives on the `192.168.123.0` subnet (from the local subnet or a remote network), and it has a destination address of `192.168.123.132`, your computer will receive it from the network and process it.

Almost all decimal subnet masks convert to binary numbers that are all ones on the left and all zeros on the right. Some other common subnet masks are:
| Decimal |	Binary
| :----------- | :---------------------------
| 255.255.255.192	| 1111111.11111111.1111111.11000000
| 255.255.255.224	| 1111111.11111111.1111111.11100000

Internet [RFC 1878](https://datatracker.ietf.org/doc/html/rfc1878) describes the valid subnets and subnet masks that can be used on TCP/IP networks.

### Network classes
Internet addresses are allocated by the InterNIC, the organization that administers the Internet. These IP addresses are divided into classes. The most common of them are classes A, B, and C. Classes D and E exist, but aren't used by end users. Each of the address classes has a different default subnet mask. You can identify the class of an IP address by looking at its first octet. Following are the ranges of Class A, B, and C Internet addresses, each with an example address:
- Class A networks use a default subnet mask of `255.0.0.0` and have `0-127` as their first octet. The address `10.52.36.11` is a class A address. Its first octet is `10`, which is between `1` and `126`, inclusive.
- Class B networks use a default subnet mask of `255.255.0.0` and have `128-191` as their first octet. The address `172.16.52.63` is a class B address. Its first octet is `172`, which is between `128` and `191`, inclusive.
- Class C networks use a default subnet mask of `255.255.255.0` and have `192-223` as their first octet. The address `192.168.123.132` is a class C address. Its first octet is `192`, which is between `192` and `223`, inclusive.

In some scenarios, the default subnet mask values don't fit the organization needs for one of the following reasons:
- The physical topology of the network
- The numbers of networks (or hosts) don't fit within the default subnet mask restrictions.

### Subnetting
A Class A, B, or C TCP/IP network can be further divided, or subnetted, by a system administrator. It becomes necessary as you reconcile the logical address scheme of the Internet (the abstract world of IP addresses and subnets) with the physical networks in use by the real world.

A system administrator who is allocated a block of IP addresses may be administering networks that aren't organized in a way that easily fits these addresses. For example, you have a wide area network with 150 hosts on three networks (in different cities) that are connected by a TCP/IP router. Each of these three networks has 50 hosts. You are allocated the class C network `192.168.123.0`. (For illustration, this address is actually from a range that isn't allocated on the Internet.) It means that you can use the addresses `192.168.123.1` to `192.168.123.254` for your 150 hosts.

Two addresses that can't be used in your example are `192.168.123.0` and `192.168.123.255` because binary addresses with a host portion of **all ones and all zeros are invalid** . The zero address is invalid because it's used to specify a network without specifying a host. The 255 address (in binary notation, a host address of all ones) is used to broadcast a message to every host on a network. Just remember that the first and last address in any network or subnet can't be assigned to any individual host.

You should now be able to give IP addresses to 254 hosts. It works fine if all 150 computers are on a single network. However, your 150 computers are on three separate physical networks. Instead of requesting more address blocks for each network, you divide your network into subnets that enable you to use one block of addresses on multiple physical networks.

In this case, you divide your network into four subnets by using a subnet mask that makes the network address larger and the possible range of host addresses smaller. In other words, you are 'borrowing' some of the bits used for the host address, and using them for the network portion of the address. The subnet mask `255.255.255.192` gives you four networks of 62 hosts each. It works because in binary notation, `255.255.255.192` is the same as `1111111.11111111.1111111.11000000`. The first two digits of the last octet become network addresses, so you get the additional networks `00000000 (0)`, `01000000 (64)`, `10000000 (128)` and `11000000 (192)`. (Some administrators will only use two of the subnetworks using `255.255.255.192` as a subnet mask. For more information on this topic, see [RFC 1878](https://datatracker.ietf.org/doc/html/rfc1878).) In these four networks, the last six binary digits can be used for host addresses.

Using a subnet mask of `255.255.255.192`, your `192.168.123.0` network then becomes the four networks `192.168.123.0`, `192.168.123.64`, `192.168.123.128` and `192.168.123.192`. These four networks would have as valid host addresses:
```
1.	192.168.123.1-62 
2.	192.168.123.65-126 
3.	192.168.123.129-190 
4.	192.168.123.193-254
```

Remember, again, that binary host addresses with all ones or all zeros are invalid, so you can't use addresses with the last octet of `0, 63, 64, 127, 128, 191, 192, or 255`.

You can see how it works by looking at two host addresses, `192.168.123.71` and `192.168.123.133`. If you used the default Class C subnet mask of `255.255.255.0`, both addresses are on the `192.168.123.0` network. However, if you use the subnet mask of `255.255.255.192`, they are on different networks; `192.168.123.71` is on the `192.168.123.64` network, `192.168.123.133` is on the `192.168.123.128` network.

Default gateways
---
If a TCP/IP computer needs to communicate with a host on another network, it will usually communicate through a device called a router. In TCP/IP terms, a router that is specified on a host, which links the host's subnet to other networks, is called a default gateway. This section explains how TCP/IP determines whether or not to send packets to its default gateway to reach another computer or device on the network.

When a host attempts to communicate with another device using TCP/IP, it performs a comparison process using the defined subnet mask and the destination IP address versus the subnet mask and its own IP address. The result of this comparison tells the computer whether the destination is a local host or a remote host.

If the result of this process determines the destination to be a local host, then the computer will send the packet on the local subnet. If the result of the comparison determines the destination to be a remote host, then the computer will forward the packet to the default gateway defined in its TCP/IP properties. It's then the responsibility of the router to forward the packet to the correct subnet.
<!--
## 🚩 Level

<details>
  <summary>Level 1</summary>
  <br>
  <img src="https://user-images.githubusercontent.com/100013115/226160244-0409be6d-ba15-4674-8e6e-a9e5b21cab75.png" alt="level1">
  <br>
  <br>

### A1: IP
Since Client A and Client B are on the same network, their IP address must represent the same network in accordance with the subnet mask. 
The subnet mask is `255.255.255.0`, which means that the first `3 bytes` of the IP address represent the network, and the 4th byte represents the host. Since we are on the same network, only the host can change. 
The solution will be anything in the range of `104.99.23.0 - 104.99.23.255` excluding the following:
~~~
104.99.23.0: The first number in the range of hosts (0 in this case) represents the network and cannot be used by a host.
104.99.23.255: The last number in the range of hosts (255 in this case) represents the broadcast address.
104.99.23.12: This address is already used by the host Client B.
~~~

### D1: IP
The same situation as A1, however the subnet mask is `255.255.0.0` in this case. The first 2 bytes of the IP address will represent the network; and the last `2 bytes`, the host address.
The solution will be anything in the range of `211.191.0.0 - 211.191.255.255`, excluding:
~~~~
211.191.0.0: Represents the network address.
211.191.255.255: Represents the broadcast address.
211.191.89.75: Already taken by host Client C.
~~~~
</br>
</details>

---
<details>
  <summary>Level 2</summary>
  <br>
  <img src="https://user-images.githubusercontent.com/100013115/226160392-e71c0077-0276-4f8c-aa60-a8af51bcf0f2.png" alt="level2">
  <br>
  <br>

### B1: Mask
Since Client B is on the same private network as Client A, they should have the exact same subnet mask. The solution can only be `255.255.255.224`.

### A1: IP
To understand the subnet mask of `255.255.255.224`, let's look at it in binary form, along with the IP `192.168.20.222` of Client B:
- MASK: 11111111.11111111.11111111.11100000
- IP:   11000000.10101000.00010100.11011101

As we can see, the first `27 bits` represent the IP address, while only the last `5 bits` represent the host address.
All these `27 bits` representing the network must stay the same in the IP addresses of hosts on the same network. To get the answer, we can only change the last `5 bits`. 

The answer is in the range of:
```
BIN:  11000000.10101000.10000001.11000000 - 11000000.10101000.10000001.11011111
or
DEC:  192.168.129.192 - 192.168.129.223
```
Excluding: 
```
11000000.10101000.10000001.11000000 (192.168.129.192): Represents the network address (notice all 0 in the last 5 bits).
11000000.10101000.10000001.11011111 (192.168.129.223): Represents the broadcast address (notice all 1 in the last 5 bits).
11000000.10101000.10000001.11011110 (192.168.129.222): Client B already has that address.
```
### C1 & D1: IP
Here we are introduced the slash "/" notation for the subnet mask on Interface D1. A subnet mask of `/30` means that the first `30 bits` of the IP address represent the network address, and the remaining `2 bits` represent the host address:

Mask /30: `11111111.11111111.11111111.11111100`
We can see that this binary number corresponds to the decimal `255.255.255.252`, therefore it is identical to the mask found on Interface C1. 

The answers can then be any address, as long as they meet the following conditions:

The network address (first 30 bits) must be identical for Client D and Client C.
The host bits (last 2 bits) cannot be all 1, nor all 0.
Client D and Client C do not have identical IP addresses.
</br>
</details>

---
<details>
  <summary>Level 3</summary>
  <br>
  <img src="https://user-images.githubusercontent.com/100013115/226161423-0af61a0c-7aae-4bb5-ba1c-e36b7d3a867b.png" alt="level3">
  <br>
  <br>
This exercise introduces the use of the switch (Switch S in this example). The switch links multiple hosts of the same network together. 

### A1 & B1: Mask
Client A, Client B, and Client C are all on the same network. Therefore, they must all have the same subnet mask. Since Client C already has the mask `255.255.255.128`, the mask for Interface B1 and for Interface A1 will also be `255.255.255.128` (or in slash notation: `/25`). 

### B1 & C1: IP
The IP address of Interface B1 and Interface C1 must be on the same network range as the IP of Client A. This range is:
```
104.198.241.0 - 104.198.241.128
```
Excluding of course the network address and the broadcast address.
</br>
</details>

---
<details>
  <summary>Level 4</summary>
  <br>
  <img src="https://user-images.githubusercontent.com/100013115/226162499-c1a6d8bf-b5c8-4714-b45b-83b7de0ffc17.png" alt="level4">
  <br>
  <br>
This exercise introduces the router. The router is used to link multiple networks together. It does so with the use of multiple interfaces (Interface R1, Interface R2, and Interface R3 in this example). 

### B1, A1 & R1: Mask
Since none of the masks on Interface B1, Interface A1, and Interface R1 are entered, we are free to choose our own subnet mask. A mask of `/24` is ideal as it leaves us with the entire 4th byte for the host address, and does not require binary calculations to find the range of possible host addresses. 

### B1 & R1: IP
The IP address of Interface B1 and Interface R1 must have the same network address as the IP address of Interface A1. With a subnet of `/24`, the possible range is:
```
72.4.110.0 - 72.4.110.255
```
Excluding the network address and the broadcast address. 

Note that we did not interact with the router Interface R2 and Interface R3, since none of our communications had to reach these sides of the router.
</br>
</details>

---
<details>
  <summary>Level 5</summary>
  <br>
  <img src="https://user-images.githubusercontent.com/100013115/226162689-aa948a49-1ae0-46b9-8ce3-d6956f3ddd4d.png" alt="level5">
  <br>
  <br>
This level introduces routes. A route contains 2 fields, the first one is the destination of outbound packets, the second one is the next hop of the packets. 

The destination default is equivalent to `0.0.0.0/0`, which will send the packets indiscriminately to the first network address it encounters. A destination address of `122.3.5.3/24` would send the packets to the network `122.3.5.0`.

The **next hop** is the IP address of the next router (or internet) interface to which the interface of the current machine must send its packets. 

Client A only has 1 route through which it can send its packets. There is no use specifying a numbered destination. The destination default will send the packets to the only path available. 

The next hop address must be the IP address of the next router's interface on the packets' way. The next interface is Interface R1, with the IP address of `44.93.252.126`. Note that the next interface is not Interface A1, since this is the sender's own interface.
</br>
</details>

---
<details>
  <summary>Level 6</summary>
  <br>
  <img src="https://user-images.githubusercontent.com/100013115/226230591-e5585e50-026a-4084-aa0c-2d8890228333.png" alt="level6">
  <br>
  <br>

</br>
</details>

---
<details>
  <summary>Level 7</summary>
  <br>
  <img src="https://user-images.githubusercontent.com/100013115/226161423-0af61a0c-7aae-4bb5-ba1c-e36b7d3a867b.png" alt="level7">
  <br>
  <br>
</br>
</details>
-->

Reference
---
[RFC 1878](https://datatracker.ietf.org/doc/html/rfc1878)

[IP Subnet Calculator](https://www.calculator.net/ip-subnet-calculator.html?cclass=any&csubnet=26&cip=124.82.129.208&ctype=ipv4&printit=0&x=66&y=39)

[Understand TCP/IP addressing and subnetting basics](https://learn.microsoft.com/en-us/troubleshoot/windows-client/networking/tcpip-addressing-and-subnetting)

[Subnet Cheat Sheet – 24 Subnet Mask, 30, 26, 27, 29, and other IP Address CIDR Network References](https://www.freecodecamp.org/news/subnet-cheat-sheet-24-subnet-mask-30-26-27-29-and-other-ip-address-cidr-network-references/)

