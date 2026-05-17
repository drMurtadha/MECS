# MECS2323: Advanced Computer Network and Cloud Computing
## Lecture Notes — Sensor Networks (Weeks 5–6)
**Universiti Teknologi Malaysia**
**Prepared by: Prof. Madya Dr. Mohd. Murtadha Bin Mohamad**

---

## Course Learning Outcomes (CLO)

By the end of this topic, students should be able to:

- **CLO1**: Describe the state-of-the-art technologies in sensor and wireless networks (C4)
- **CLO3**: Agree among a team on solutions to current problems in sensor network deployments (TS5)

---

## 1. Introduction to Wireless Sensor Networks (WSN)

### 1.1 What Is a Wireless Sensor Network?

A **Wireless Sensor Network (WSN)** is a distributed collection of small, autonomous devices — called **sensor nodes** or **motes** — that monitor physical or environmental conditions (temperature, sound, pressure, motion, etc.) and transmit data wirelessly to a central point called a **base station** or **sink**.

WSNs bridge the physical world and the digital world. They allow us to collect real-time data from environments that are difficult, dangerous, or impractical for humans to access continuously — deep-sea floors, forest fire zones, industrial machinery, or the human body.

### 1.2 A Brief History

| Era | Milestone |
|-----|-----------|
| 1970s–1980s | Military surveillance networks (DARPA's Distributed Sensor Networks project) |
| 1990s | Smart Dust concept by UC Berkeley — motes the size of a matchbox |
| Early 2000s | TinyOS and open-source sensor platforms (MicaZ, TelosB motes) |
| 2010s | Rise of IoT; WSNs integrated into smart homes, agriculture, healthcare |
| 2020s | Software-Defined WSN, AI-assisted sensing, integration with 5G and edge computing |

### 1.3 Key Characteristics of WSNs

- **Resource-constrained**: Nodes have limited processing power, memory, and battery life.
- **Self-organizing**: Nodes form networks dynamically without pre-configured infrastructure.
- **Dense deployment**: Hundreds or thousands of nodes may be deployed in a single area.
- **Fault-tolerant**: The network should continue operating even if individual nodes fail.
- **Application-specific**: WSN protocols and designs are often tailored to a particular use case.
- **Data-centric**: Unlike IP networks, WSNs are less concerned with node addresses and more concerned with *what data* is being reported.

---

## 2. WSN Architecture

### 2.1 Sensor Node Components

Each sensor node typically contains four key subsystems:

```
┌─────────────────────────────────────────────┐
│               SENSOR NODE                   │
│  ┌───────────┐  ┌──────────┐  ┌──────────┐  │
│  │  Sensing  │  │ Processor│  │  Radio   │  │
│  │  Unit     │→ │  Unit    │→ │  Unit    │  │
│  │ (sensors) │  │(MCU+mem) │  │(TX/RX)   │  │
│  └───────────┘  └──────────┘  └──────────┘  │
│               ┌──────────┐                  │
│               │  Power   │                  │
│               │  Unit    │                  │
│               │(battery) │                  │
│               └──────────┘                  │
└─────────────────────────────────────────────┘
```

| Subsystem | Function | Examples |
|-----------|----------|----------|
| Sensing Unit | Measures physical parameters | Temperature (DHT22), humidity, accelerometer, camera |
| Processing Unit | Runs the OS and protocols | ATmega128, ARM Cortex-M |
| Radio Unit | Wireless communication | IEEE 802.15.4 (Zigbee), Bluetooth LE, LoRa |
| Power Unit | Powers the node | AA batteries, solar cells, energy harvesting |

### 2.2 Network Topologies

WSNs can be organized in several topologies:

**Star Topology**
All sensor nodes communicate directly with a central gateway. Simple but creates a single point of failure; works well for short-range deployments.

**Mesh Topology**
Nodes relay data for each other (multi-hop routing). More resilient and covers larger areas. Requires more complex routing protocols (e.g., RPL for IPv6-based WSNs).

**Cluster-Tree (Hierarchical) Topology**
Nodes are grouped into clusters, each with a **cluster head** (CH) that aggregates data before forwarding to the base station. Reduces energy consumption at ordinary nodes.

```
                 [Base Station]
                      |
          ┌───────────┴──────────┐
        [CH1]                 [CH2]
       /  |  \               /  |  \
     N1   N2  N3           N4  N5   N6
```

### 2.3 Protocol Stack

The WSN protocol stack mirrors the OSI model but is optimized for constrained environments:

| Layer | Protocol Examples | Purpose |
|-------|-------------------|---------|
| Application | TinyDB, Deluge, CoAP | Data querying, code update, RESTful API |
| Transport | SNACK, PSFQ | Reliable delivery (lightweight) |
| Network | RPL, LEACH | Routing and topology management |
| Data Link | IEEE 802.15.4 MAC | Media access control, TDMA/CSMA |
| Physical | IEEE 802.15.4 PHY | 2.4 GHz ISM band, 250 kbps |

Cross-layer optimization is common — e.g., the MAC layer is informed of remaining battery level to adjust duty-cycling.

---

## 3. Types of Sensor Networks

### 3.1 Terrestrial WSN
The most common type. Nodes are deployed on land (outdoor fields, indoor environments). Used in agriculture, smart cities, industrial monitoring.

### 3.2 Underground WSN
Nodes are buried in the soil. Used to monitor soil moisture, detect seismic activity, or track pipeline leaks. Main challenge: signal attenuation through soil.

### 3.3 Underwater WSN (UW-WSN)
Nodes are deployed underwater — in oceans, lakes, or rivers. Radio waves do not propagate well underwater, so **acoustic communication** is commonly used instead.

> **Reference**: Okereke, C., Wahab, N.H.A., **Mohamad, M.M.**, Zaleha, S.H. (2021). *Autonomous Underwater Vehicle in Internet of Underwater Things: A Survey*. Journal of Physics: Conference Series. [8 citations, FWCI: 3.60]

Applications include oceanographic data collection, oil spill detection, and tracking of autonomous underwater vehicles (AUVs).

### 3.4 Multimedia WSN
Nodes are equipped with cameras, microphones, or other multimedia sensors. Used in surveillance, traffic monitoring, and wildlife observation. High bandwidth demand.

### 3.5 Mobile WSN
Unlike traditional static deployments, mobile WSNs include nodes that can move — mounted on robots, vehicles, or animals. This improves coverage but complicates routing.

### 3.6 Body Area Network (BAN) / Body Sensor Network (BSN)
Sensors worn on or implanted in the human body. Used for health monitoring — ECG, blood glucose, body temperature, posture. Governed by IEEE 802.15.6.

---

## 4. Key Challenges in WSN Design

### 4.1 Energy Efficiency
This is the dominant challenge. Sensor nodes are typically battery-powered and deployed in remote locations where battery replacement is difficult or impossible.

**Strategies:**
- **Duty cycling**: Nodes sleep most of the time and wake up only to sense/transmit.
- **Data aggregation**: Cluster heads combine data from multiple nodes before forwarding, reducing the number of transmissions.
- **Energy harvesting**: Solar panels, piezoelectric materials, or RF energy.

### 4.2 Scalability
A WSN might grow from 10 nodes to 10,000. Protocols must scale without dramatically increasing overhead. Hierarchical clustering (e.g., LEACH, HEED) addresses this.

### 4.3 Reliability and Fault Tolerance
Nodes may fail due to battery depletion, hardware faults, or environmental damage. The network must detect failures and reroute data automatically.

### 4.4 Security
WSNs are vulnerable to several attacks:

| Attack Type | Description |
|-------------|-------------|
| Eavesdropping | Passive interception of transmitted data |
| Sinkhole attack | Malicious node attracts traffic and drops packets |
| Sybil attack | A node claims multiple false identities |
| Denial of Service (DoS) | Flooding the network with spurious requests |
| Physical tampering | Physical capture and reprogramming of nodes |

> **Reference**: Basharat, A., **Mohamad, M.M.B.** (2022). *Security Challenges and Solutions for Internet of Things based Smart Agriculture: A Review*. 4th ICSSA. [17 citations, FWCI: 3.72]

**Security countermeasures** include lightweight cryptography (AES-128, ECC), secure key management, and anomaly detection using machine learning.

### 4.5 Data Management and Quality
Raw sensor data is noisy. Techniques such as **data fusion**, **outlier detection**, and **in-network processing** help ensure data quality before transmission.

### 4.6 Connectivity and Coverage
The network must maintain connectivity (every node can communicate, directly or through others) while ensuring that the sensing area is fully covered. Deployment strategies and topology control algorithms address this.

---

## 5. Routing Protocols in WSN

### 5.1 Data-Centric Protocols
Instead of routing by node address, nodes route by *data content*.
- **Directed Diffusion**: A sink floods the network with "interests" (queries). Nodes with matching data send it back. Gradients are reinforced over time.

### 5.2 Hierarchical Protocols
- **LEACH (Low-Energy Adaptive Clustering Hierarchy)**: Nodes randomly rotate the role of cluster head to distribute energy load. Simple and widely cited.
- **HEED**: Selects cluster heads based on residual energy and communication cost.

### 5.3 Location-Based Protocols
Nodes use GPS or other positioning to make routing decisions.
- **GEAR (Geographical and Energy Aware Routing)**: Routes data towards geographic regions of interest.

### 5.4 QoS-Aware Protocols
Prioritize time-sensitive data (e.g., fire alarm) over routine readings.

---

## 6. Software-Defined Wireless Sensor Networks (SD-WSN)

### 6.1 Motivation
Traditional WSNs are difficult to manage and reconfigure. Each application requires a different firmware. Software-Defined Networking (SDN) principles — separating the **control plane** from the **data plane** — can be applied to WSNs to make them more flexible and manageable.

### 6.2 SD-WSN Architecture

```
┌──────────────────────────────────────────────┐
│               APPLICATION LAYER              │
│   (Network Management, Security, Analytics)  │
└──────────────────┬───────────────────────────┘
                   │ Northbound API
┌──────────────────┴───────────────────────────┐
│               CONTROL PLANE                  │
│        (SDN Controller: OpenDaylight,        │
│         ONOS, or custom WSN controller)      │
└──────────────────┬───────────────────────────┘
                   │ Southbound API (OpenFlow-like)
┌──────────────────┴───────────────────────────┐
│               DATA PLANE                     │
│      (Sensor nodes — constrained devices)    │
└──────────────────────────────────────────────┘
```

### 6.3 Benefits of SD-WSN
- **Centralized network view**: The controller has a global view of the network topology and can make optimal routing decisions.
- **Programmability**: Network behavior can be changed without re-flashing individual nodes.
- **Scalability**: The controller manages routing tables for all nodes.
- **Security**: Centralized policy enforcement.

### 6.4 Challenges of SD-WSN
- **Controller overhead**: Communication between nodes and controller adds traffic.
- **Latency**: Real-time applications may be affected.
- **Fault tolerance**: What happens if the controller fails?
- **Constrained nodes**: Implementing SDN abstractions on memory-limited microcontrollers is non-trivial.

> **Reference**: Alsaeedi, M., **Mohamad, M.M.**, Al-Roubaiey, A. (2024). *SSDWSN: A Scalable Software-Defined Wireless Sensor Networks*. IEEE Access. [12 citations, FWCI: 1.24]

SSDWSN presents a scalable SD-WSN framework that addresses the overhead and scalability issues by designing a lightweight southbound protocol and an efficient controller placement strategy.

---

## 7. WSN Applications

### 7.1 Smart Agriculture
Sensors monitor soil moisture, temperature, humidity, and nutrient levels. Farmers can receive real-time alerts and automate irrigation. Drones equipped with sensors survey large fields.

**Key concern**: Security. Sensor data in agricultural systems may be intercepted or manipulated, leading to crop damage or financial loss.

> **Reference**: Basharat, A., **Mohamad, M.M.B.** (2022). *Security Challenges and Solutions for Internet of Things based Smart Agriculture: A Review*. ICSSA 2022.

### 7.2 Building Fire Detection
Smoke detectors and temperature sensors can form a WSN to provide early fire warning. AI models can be trained to distinguish actual fires from false alarms (burnt toast vs. structural fire).

> **Reference**: Wahyono, I.D., Asfani, K., **Mohamad, M.M.**, Afandi, A.N., Aripriharta, A. (2020). *The New Intelligent Wireless Sensor Network using Artificial Intelligence for Building Fire Disasters*. ICVEE 2020. [8 citations]

> **Reference**: Wahyono, I.D., Asfani, K., **Mohamad, M.M.**, Afandi, A.N., Aripriharta, A. (2020). *New Hybrid Algorithm Implementation on spread Wireless Sensor to determine the point of fire in the building*. ICITACEE 2020. [3 citations]

The hybrid algorithm uses a combination of sensor readings and spatial distribution to **locate the origin point of the fire** — not just detect it, but pinpoint it in the building layout.

### 7.3 Environmental and Ocean Monitoring
Underwater sensor nodes track water temperature gradients, currents, and marine biodiversity. AUVs navigate autonomously and relay data to surface buoys.

> **Reference**: Okereke, C., Wahab, N.H.A., **Mohamad, M.M.**, Zaleha, S.H. (2021). *Autonomous Underwater Vehicle in Internet of Underwater Things: A Survey*. Journal of Physics. [8 citations, FWCI: 3.60]

### 7.4 Healthcare and Wearables
BSNs monitor patient vital signs continuously. Elderly fall detection, medication reminders, and cardiac event alerting are enabled by body-worn sensors.

### 7.5 Industrial IoT (IIoT)
Sensors monitor vibration, temperature, and pressure in machines (predictive maintenance). WSNs in factories reduce downtime by alerting maintenance teams before equipment fails.

### 7.6 Smart Cities
Street lighting, waste bin fill-level monitoring, parking spot detection, traffic flow measurement — all enabled by distributed sensor nodes embedded in urban infrastructure.

---

## 8. Emerging Trends

### 8.1 Artificial Intelligence in WSN
Machine learning models (CNNs, RNNs, reinforcement learning) can be deployed at the edge to process sensor data locally — reducing the amount of raw data that needs to be transmitted and enabling faster responses.

**TinyML**: Running ML inference on microcontrollers (e.g., TensorFlow Lite Micro on an Arduino). A sensor node can classify data locally before deciding whether to send an alert.

### 8.2 Integration with 5G
5G's ultra-reliable low-latency communication (URLLC) enables WSNs for mission-critical applications. Massive machine-type communications (mMTC) allow millions of IoT devices per km².

### 8.3 Energy Harvesting
Beyond solar, next-generation nodes harvest energy from:
- **Vibration** (piezoelectric materials in industrial environments)
- **RF energy** (ambient WiFi/cellular signals)
- **Thermal gradients** (body heat in wearables)

### 8.4 Blockchain for WSN Security
Decentralized ledgers can provide tamper-proof data provenance in WSNs — particularly useful in smart agriculture or supply chain monitoring where data authenticity is critical.

### 8.5 Digital Twins
A **digital twin** is a virtual replica of a physical system. WSN data feeds a real-time simulation of a building, factory, or environment — enabling predictive analysis and scenario testing.

---

## 9. Summary

| Topic | Key Point |
|-------|-----------|
| WSN Definition | Distributed autonomous nodes sensing and communicating wirelessly |
| Architecture | Sensing + Processing + Radio + Power; organized in star/mesh/cluster topologies |
| Challenges | Energy, scalability, security, reliability, data quality |
| Routing | Data-centric (Directed Diffusion), hierarchical (LEACH), location-based (GEAR) |
| SD-WSN | SDN principles applied to WSN for programmability and scalability |
| Applications | Agriculture, fire detection, underwater, healthcare, smart cities |
| Trends | AI/TinyML, 5G integration, energy harvesting, blockchain, digital twins |

---

## 10. Self-Assessment Questions

1. What are the four main components of a sensor node? Describe the trade-off between processing capability and energy consumption.
2. Compare star, mesh, and cluster-tree topologies for a large-scale agricultural WSN. Which would you recommend and why?
3. Explain the sinkhole attack. How would you detect and mitigate it?
4. What is SD-WSN? What problem does it solve compared to traditional WSN management?
5. A company wants to deploy a WSN to detect fires in a multi-storey building. Identify three key challenges and propose technical solutions for each. (Refer to Wahyono et al., 2020)
6. Based on the SSDWSN paper (Alsaeedi, Mohamad & Al-Roubaiey, 2024), explain what makes it "scalable" compared to earlier SD-WSN approaches.

---

## References

1. Alsaeedi, M., Mohamad, M.M., & Al-Roubaiey, A. (2024). SSDWSN: A Scalable Software-Defined Wireless Sensor Networks. *IEEE Access*. https://doi.org/10.1109/ACCESS.2024

2. Basharat, A., & Mohamad, M.M.B. (2022). Security Challenges and Solutions for Internet of Things based Smart Agriculture: A Review. *4th International Conference on Smart Sensors and Application (ICSSA 2022)*.

3. Okereke, C., Wahab, N.H.A., Mohamad, M.M., & Zaleha, S.H. (2021). Autonomous Underwater Vehicle in Internet of Underwater Things: A Survey. *Journal of Physics: Conference Series*.

4. Wahyono, I.D., Asfani, K., Mohamad, M.M., Afandi, A.N., & Aripriharta, A. (2020). The New Intelligent Wireless Sensor Network using Artificial Intelligence for Building Fire Disasters. *ICVEE 2020 Proceedings*.

5. Wahyono, I.D., Asfani, K., Mohamad, M.M., Afandi, A.N., & Aripriharta, A. (2020). New Hybrid Algorithm Implementation on spread Wireless Sensor to determine the point of fire in the building. *ICITACEE 2020 Proceedings*.

6. Akyildiz, I.F., Su, W., Sankarasubramaniam, Y., & Cayirci, E. (2002). Wireless sensor networks: a survey. *Computer Networks*, 38(4), 393–422.

7. Kurose, J., & Ross, K. (2017). *Computer Networking: A Top-Down Approach* (7th ed.). Pearson Education.

8. Sallis, P.J. (2017). *Wireless Sensor Networks: Insights and Innovations*. BoD.

---

*These lecture notes are for educational purposes only within MECS2323. Do not distribute or reproduce without permission.*
