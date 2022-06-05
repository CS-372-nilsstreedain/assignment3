# Assignment 3
1. Consider a datagram network using 32-bit host addresses. Suppose a router has four links, numbered 0 through 3, and packets are to be forwarded to the link interfaces as follows:

Destination Address Range	| Link Interface
-|-
11100000 00000000 00000000 00000000 through 11100000 00111111 11111111 11111111 |	0
11100000 01000000 00000000 00000000 through 11100000 01000000 11111111 11111111 |	1
11100000 01000001 00000000 00000000 through 11100001 01111111 11111111 11111111 |	2
otherwise	| 3

  - Provide a forwarding table that has five entries, uses longest prefix matching, and forwards packets to the correct link interfaces.

Prefix Match | Link Interface
-|-
11100000 00	| 0
11100000 01000000	| 1
1110000	| 2
11100001 1 | 3
otherwise	| 3

  - Describe how your forwarding table determines the appropriate link interface for datagrams with destination addresses:
```
11001000 10010001 01010001 01010101
11100001 01000000 11000011 00111100
11100001 10000000 00010001 01110111

First address is interface 3, because it doesn’t match any prefix.
Second address is interface 2 because the prefix matches 1110000.
Third address is interface 3 because the prefix matches 11100001 1.
```

2. Consider a datagram network using 8-bit host addresses. Suppose a router uses longest prefix matching and has the forwarding table in Table 2: For each of the four interfaces, give the associated range of destination host addresses and the number of addresses in the range.
Prefix Match | Interface
-|-
00 | 0
010	| 1
011	| 2
10	| 2
11	| 3

```
00   | 00111111 - 00000000 = 111111 => 64
010 | 01011111 - 01000000 = 11111 => 32
011 | 01111111 - 01100000 = 11111 => 32
10   | 10111111 - 10000000 = 111111 => 64
11   | 11111111 - 11000000 = 111111 => 64
interface 0: 00 => 64
interface 1: 010 => 32
interface 2: 011 + 10 => 96
interface 3: 11 => 64
```

3. Consider a datagram network using 8-bit host addresses. Suppose a router uses longest prefix matching and has the forwarding table in Table 3:  For each of the four interfaces, give the associated range of destination host addresses and the number of addresses in the range.
Prefix Match | Interface
-|-
1	| 0
10 | 1
111 | 2
otherwise	| 3

```
1 | 11111111 - 10000000 = 1111111 => 128
10 | 10111111 - 10000000 = 111111 => 64
111 | 11111111 - 11100000 = 11111 => 32
Other | 01111111 - 0000000 = 1111111 => 128
Interface 0: 128
Interface 1: 64
Interface 2: 32
Interface 3: 128
```

4. Consider a router that interconnects three subnets: Subnet 1, Subnet 2, and Subnet 3. Suppose all of the interfaces in each of these three subnets are required to have the prefix 223.1.17/24. Also suppose that Subnet 1 is required to support at least 60 interfaces, Subnet 2 is to support at least 90 interfaces, and Subnet 3 is to support at least 12 interfaces. Provide three network addresses (of the form a.b.c.d/x) that satisfy these constraints.
```
Subnet 1: 223.1.17.0/26
Subnet 2: 223.1.17.128/25
Subnet 3: 223.1.17.64/28

Subnet 2: 223:1.17.0/25
Subnet 1: 223.1.17.128/26
Subnet 3: 223.1.17.192/28
```

5. Consider a subnet with prefix 128.119.40.128/26. Give an example of one IP address (of form xxx.xxx.xxx.xxx) that can be assigned to this network. Suppose anISP owns the block of addresses of the form 128.119.40.64/26. Suppose it wants to create four subnets from this block, with each block having the same number of IP addresses. What are the prefixes (of form a.b.c.d/x) for the four subnets?
```
One IP: 128.119.40.129

Subnet 1: 128.119.40.64/28
Subnet 2: 128.119.40.80/28
Subnet 3: 128.119.40.96/28
Subnet 4: 128.119.40.112/28
```

6. Consider the network in Figure 1. With the indicated link costs, use Dijkstras shortest-path algorithm to compute the shortest path from x to all network nodes. Show how the algorithm works by computing a table.
<img width="208" alt="image" src="https://user-images.githubusercontent.com/25465133/172073317-af981fc8-284a-4b07-b7c8-5b9439e9d88d.png">

Step | N’ | T | U | V | W | Y | Z
-|-|-|-|-|-|-|-
0 | x | ∞ | ∞ | 3, x | 6, x | 6, x | 8, x
1 | xv | 7, v | 6, v | 3, x | 6, x | 6, x | 8, x
2 | xvu | 7, v | 6, v | 3, x | 6, x | 6, x | 8, x
3 | xvuw | 7, v | 6, v | 3, x | 6, x | 6, x | 8, x
4 | xvuwy | 7, v | 6, v | 3, x | 6, x | 6, x | 8, x
5 | xvuwyt | 7, v | 6, v | 3, x | 6, x | 6, x | 8, x
6 | xvuwytz | 7, v | 6, v | 3, x | 6, x | 6, x | 8, x

7. Consider the network shown in Figure 2, and assume that each node initially knows the costs to each of its neighbors. Consider the distance-vector algorithm and show the distance table entries at node z.
<img width="203" alt="image" src="https://user-images.githubusercontent.com/25465133/172073407-0fe7e06c-0086-4d36-a998-6b088eb71c08.png">

Step 1 | U | V | X | Y | Z
-|-|-|-|-|-
V
X
Z |  | 6 | 2 |  | 0

Step 2 | U | V | X | Y | Z
-|-|-|-|-|-
V | 1 | 0 | 3 |  | 6
X |  | 3 | 0 | 3 | 2
Z | 7 | 5 | 2 | 5 | 0

Step 3 | U | V | X | Y | Z
-|-|-|-|-|-
X | 1 | 0 | 3 | 3 | 5
Y | 4 | 3 | 0 | 3 | 2
Z | 6 | 5 | 2 | 5 | 0
