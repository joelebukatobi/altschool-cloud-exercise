## Month Two

---

### Week Five / Exercise Nine

In week five we talked about Networking and its many abstracts including IP Addressing.
Networking, according to [Tech Target](https://www.techtarget.com/searchnetworking/definition/networking) also known as computer networking, is the practice of transporting and exchanging data between nodes over a shared medium in an information system. Networking comprises not only the design, construction and use of a network, but also the management, maintenance and operation of the network infrastructure, software and policies.

For exercise nine we were given the following IP Address with a Subnet Mask: **193.16.20.35/29** and asked to get the following.

- What is the Network IP
- Number of hosts
- Range of IP Addresses
- Broadcast IP from this Subnet

<!-- ## [Subnet Verification Link](https://www.calculator.net/ip-subnet-calculator.html) click me! -->

### Procedure

IN order to find the above listed entities with the given IP Address 193.16.20.35 with a subnet mask 255.255.255.248 or /29. We would first of all need to do the following

- Convert to Binary
- Calculate the Subset Address
- Find the number of Host
- Calculate the range of IP Addresses

#### Step One: Convert to binary

| IP Address (Decimal) | 193      | 16       | 20       | 35       |
| -------------------- | -------- | -------- | -------- | -------- |
| IP Address (Binary)  | 11000001 | 00010000 | 00010100 | 00100011 |
| Subnet Mask Decimal  | 255      | 255      | 255      | 248      |
| Subnet Mask Binary   | 11111111 | 11111111 | 11111111 | 11111000 |

#### Calculate the Network ID

To find the Network ID, we will need to perform a binary and operation on the host given IP Address and Subnet Mask. The result is the Network ID as shown below

| IP Address (Decimal)     | 193      | 16       | 20       | 35       |
| ------------------------ | -------- | -------- | -------- | -------- |
| IP Address (Binary)      | 11000001 | 00010000 | 00010100 | 00100011 |
| Subnet Mask Binary       | 11111111 | 11111111 | 11111111 | 11111000 |
| ------------------------ | -------- | -------- | -------- | -------- |
| Subnet Address (Binary)  | 11000001 | 00010000 | 00010100 | 0010000  |
| Subnet Address (Decimal) | 193      | 16       | 20       | 32       |

#### Find the number of hosts

Number of Hosts = 2^<sup>n</sup> - 2

Where **n** = number of host bits minus two

> Note
> number of host bits - 2

Counting the number of host's bits (0's) in the subnet mask binary starting from the right, which has a total of **3**

Number of hosts = 2^<sup>3</sup> - 2

> Note
> 8 - 2 = 6

#### Calculate the range IP Address

We can now calculate the range of IP Addresses and the Broadcast. Bear in mind that the First & Last IP Address is reserved for the Network and Broadcast

> Note
> **Given IP:** 193.16.20.35/29
> **Network IP:** 193.16.20.32
> **Number of Hosts:** 6
> **Range of IP Addresses:** 193.16.20.33 - 193.16.20.38
> **- min range of IP's** = 193.16.20.33
> **- max range of IP's** = 193.16.20.38
> **Broadcast IP: 193.16.20.39** -->
