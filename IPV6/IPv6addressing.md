**1.2 IPv6 addressing.md**

**IPv6 addresses structure**. 

1. **Length and Notation**:
    
    - An IPv6 address is **128 bits** long, which is a significant upgrade from the 32-bit IPv4 addresses.
    - It is represented as **eight groups** of four hexadecimal digits, separated by colons. For example: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`.
    - Hexadecimal characters are **case-insensitive**, so both uppercase and lowercase representations are equivalent.
2. **Binary to Hexadecimal Conversion**:
    
    - The 128 binary bits are divided into **eight 16-bit segments**.
    - Each 16-bit segment is converted into a **4-digit hexadecimal number**.
    - The resulting address consists of **32 characters** (including colons).
3. **Abbreviations**:
    
    - To simplify representation, IPv6 supports two types of abbreviations:
        - **Leading Zero Compression**: Allows skipping leading zeros within a nibble. For example, `2001:0db8` can be shortened to `2001:db8`.
        - **Zero Compression**: Allows dropping nibbles that contain only zeros. For instance, `::1` represents `0000:0000:0000:0000:0000:0000:0000:0001`.

The use of colons:

1. **Hexadecimal Representation**:
    
    - In IPv6, addresses are expressed using **hexadecimal notation**.
    - Hexadecimal (or hex) is a base-16 numbering system that uses digits from 0 to 9 and letters from A to F.
    - Each group of four bits (half a byte) corresponds to a single hexadecimal digit.
    - For example:
        - Binary: `11011011` (8 bits)
        - Hexadecimal: `DB` (2 digits)
2. **IPv6 Address Structure**:
    
    - An IPv6 address consists of **eight 16-bit segments**, totaling 128 bits.
    - These segments are separated by **colons**.
    - Example IPv6 address: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`.
3. **Leading Zero Compression**:
    
    - To simplify representation, leading zeros within a segment can be omitted.
    - For instance:
        - `2001:0db8` can be shortened to `2001:db8`.
4. **Zero Compression**:
    
    - When consecutive segments contain only zeros, they can be replaced with a double colon (`::`).
    - Example:
        - `2001:0:0:0:0:0:0:1` can be further shortened to `2001::1`.
5. **Case-Insensitive**:
    
    - Hexadecimal characters are **case-insensitive**.
    - Both uppercase and lowercase representations are equivalent.

Types of **IPv6 addresses**:

1. **Unicast Addresses**:
    
    - A **unicast address** represents a single interface in the network.
    - It is used for **one-to-one communication** between two devices.
    - Packets sent to a unicast address are delivered to the specific interface configured with that IPv6 address.
    - Unicast addresses include:
        - **Global Unicast Address**: Used for communication across the entire Internet.
        - **Unique Local Address (ULA)**: Used for private networks within an organization.
        - **Link-Local Address**: Used for communication within a local network segment.
2. **Multicast Addresses**:
    
    - A **multicast address** represents a dynamic group of hosts interested in the same traffic.
    - Packets sent to a multicast address are delivered to **all interfaces** identified by that address.
    - It enables **one-to-many communication**.
    - Multicast addresses include:
        - **Permanent Multicast Address**: Used for well-known groups (e.g., all routers).
        - **Transient Multicast Address**: Used for temporary groups (e.g., multimedia sessions).
        - **Solicited-Node Multicast Address**: Used for neighbor discovery.
3. **Anycast Addresses**:
    
    - An **anycast address** identifies a set of interfaces that support the same function.
    - Packets sent to an anycast address are delivered to the **nearest** interface identified by that address.
    - It enables **one-to-closest communication**.
    - Anycast is often used for services like DNS or load balancing.

