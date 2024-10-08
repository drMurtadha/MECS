**1.3 Address configuration**

Methods for configuring **IPv6 addresses**:

1. **Stateless Address Autoconfiguration (SLAAC)**:
    
    - SLAAC is a fundamental mechanism that allows devices to **automatically configure their own IPv6 addresses** and other network parameters without manual configuration or a central DHCP server.
    - How it works:
        - When an IPv6 node connects to a network, it **auto-configures a link-local address**. This address enables communication within the local segment.
        - The most common method for auto-configuring a link-local address is by combining the link-local prefix `FE80::/64` with the **EUI-64 interface identifier**, generated from the interface’s MAC address.
        - SLAAC does not require a central server to track address assignments.
        - Nodes use **Duplicate Address Detection (DAD)** to avoid address conflicts.
    - Pros:
        - Simplicity and efficiency.
        - No need for a DHCP server.
    - Cons:
        - Does not provide DNS server addresses.
        - Not widely adopted due to this limitation.
2. **Dynamic Host Configuration Protocol version 6 (DHCPv6)**:
    
    - DHCPv6 is widely adopted for dynamically assigning addresses to hosts.
    - How it works:
        - Requires a **DHCP server** on the network.
        - Provides both **stateful** and **stateless** address assignment.
        - Stateful assignment involves a server tracking address assignments, managing address pools, and resolving conflicts.
        - Stateless assignment means no server tracks assignments; nodes handle address conflicts.
    - Pros:
        - Provides DNS server addresses.
        - More control over address assignment.
    - Cons:
        - Requires additional configuration and maintenance of DHCP servers.


---

## IPv6 Privacy Extensions

IPv6 Privacy Extensions, as defined in RFC 4941, are a mechanism that generates temporary addresses which change at regular intervals. These extensions provide protection against address correlation, a technique that can expose a user’s identity and location. Different network managers offer various options to enable or disable IPv6 Privacy Extensions. The main purpose of these extensions is to minimize the potential for tracking and profiling of devices based on their IPv6 addresses.

---

## IPv6 Temporary Addresses

Temporary addresses in IPv6 are interface identifiers that offer a degree of anonymity. These addresses are randomly generated and change over time. Some operating systems, such as Windows, enable temporary IPv6 addresses by default. This means that the IPv6 address of a computer with this feature will change over time. Temporary addresses are especially relevant for mobile devices that frequently connect to different networks. By changing temporary addresses regularly, devices can reduce the chances of being tracked based on their IPv6 addresses.

---

