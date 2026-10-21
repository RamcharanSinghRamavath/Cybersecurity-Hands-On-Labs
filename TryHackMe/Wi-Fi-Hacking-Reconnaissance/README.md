
# TryHackMe: Wi-Fi Hacking

## 1. Lab Overview

**Platform:** TryHackMe  
**Room:** Wi-Fi Hacking  
**Category:** Wireless Network Security  
**Purpose:** To understand how Wi-Fi networks communicate, how IEEE 802.11 frames work, and how wireless activity can be analyzed in an authorized lab environment.

This document records the concepts learned from the first three tasks of the room. It focuses on wireless networking fundamentals, frame types, and the importance of understanding wireless traffic during a security investigation.

---

# Task 1: Introduction

## Objective

The objective of this task is to introduce wireless network security and explain why understanding Wi-Fi communication is important for cybersecurity professionals.

## What Is Wi-Fi?

Wi-Fi is a wireless networking technology that allows devices such as laptops, smartphones, and tablets to communicate over radio waves instead of requiring a physical Ethernet cable.

Wi-Fi networks are commonly used in homes, offices, educational institutions, and enterprise environments.

## Why Is Wi-Fi Security Important?

Wireless networks transmit data through radio signals. Devices within radio range may be able to observe wireless transmissions, depending on the network configuration, encryption, hardware, and capture setup.

Security professionals study wireless traffic to understand network behavior and identify suspicious activity.

Examples of wireless security concerns include:

- Unauthorized devices connecting to a network.
- Weak wireless authentication or encryption configurations.
- Deauthentication attacks that disrupt wireless connectivity.
- Rogue access points impersonating legitimate networks.
- Misconfigured access points and insecure wireless settings.

## Role of a Cybersecurity Analyst

A cybersecurity analyst may investigate wireless-related incidents by:

1. Identifying authorized wireless access points.
2. Reviewing available wireless traffic captures.
3. Understanding the behavior of connected stations.
4. Investigating unusual disconnections or suspicious management frames.
5. Documenting findings and recommending appropriate security controls.

## Key Learnings

- Wi-Fi uses radio communication to connect devices.
- Wireless security requires understanding both network configuration and wireless traffic.
- Wireless traffic analysis can support security investigations.
- Testing must be performed only on networks for which authorization has been provided.

---

# Task 2: How Wi-Fi Works

## Objective

Understand the basic architecture of a Wi-Fi network, the devices involved in wireless communication, and the identifiers used to recognize wireless networks.

## 2.1 IEEE 802.11

IEEE 802.11 is a family of standards that defines how wireless local area networks communicate.

It specifies important aspects of wireless communication, including frame formats, medium access, and management procedures.

When analyzing Wi-Fi traffic, the captured packets are commonly examined as IEEE 802.11 frames.

## 2.2 Wireless Access Point (AP)

An Access Point provides wireless connectivity to client devices and commonly connects the wireless network to a wired network.

Example:
- A company Wi-Fi router provides wireless access to employee laptops.
- The access point advertises the network so compatible devices can discover it.

## 2.3 Wireless Station (STA)

A Station is a device that participates in a wireless network.

Examples include:
- Laptop
- Smartphone
- Tablet
- Wireless-enabled computer

A station can discover access points, authenticate, associate with a network, and exchange data when the required conditions are met.

## 2.4 SSID and ESSID

**SSID (Service Set Identifier)** is the name used to identify a Wi-Fi network.

Example:
`Office-WiFi`

An ESSID is commonly used to refer to the network name of an Extended Service Set, where multiple access points may provide access to the same logical wireless network.

Important:
The SSID is a human-readable network name. It is not a password and does not provide encryption by itself.

## 2.5 BSSID

**BSSID (Basic Service Set Identifier)** identifies a particular Basic Service Set. In common infrastructure Wi-Fi deployments, it is usually represented by the MAC address of the access point's wireless interface.

Example:
`AA:BB:CC:11:22:33`

A network with multiple access points may use the same SSID but have different BSSIDs.

### SSID vs BSSID

| Feature | SSID | BSSID |
|---|---|---|
| Meaning | Wireless network name | Identifier of a specific Basic Service Set |
| Example | Office-WiFi | AA:BB:CC:11:22:33 |
| Purpose | Helps users recognize a network | Helps distinguish wireless service sets |
| Can multiple APs share it? | Yes | Each BSS normally has its own BSSID |

## 2.6 Basic Service Set (BSS)

A Basic Service Set is a fundamental building block of an IEEE 802.11 wireless network.

In a typical infrastructure BSS, an access point and its associated stations form the wireless service set.

An Extended Service Set (ESS) can connect multiple BSSs to provide broader coverage under a common network identity.

## 2.7 Wi-Fi Frequency Bands

Wi-Fi operates in different radio frequency bands, depending on the standard, region, and equipment.

Common bands include:

- **2.4 GHz:** Often offers broader coverage, but may experience more interference.
- **5 GHz:** Offers additional channel options and can support higher performance, depending on conditions.
- **6 GHz:** Available with supported Wi-Fi generations and devices in regions where permitted.

The exact channels and permitted frequencies depend on local regulations.

## 2.8 Wi-Fi Channels

A channel is a portion of the frequency spectrum used for wireless communication.

Nearby networks using overlapping channels may experience interference.

Security analysts should understand channels because the selected channel and the wireless adapter's capabilities affect which transmissions can be captured.

## 2.9 Monitor Mode

Monitor mode is a wireless adapter operating mode that can allow compatible hardware to capture 802.11 frames in its radio range without requiring the adapter to associate with the target access point.

Monitor mode does not automatically guarantee that every wireless packet can be captured. Results depend on adapter support, channel selection, signal strength, encryption, and other factors.

## 2.10 Why These Concepts Matter in Security

Understanding wireless network identifiers and architecture helps an analyst:

- Distinguish networks that share the same SSID.
- Recognize access points and stations in packet captures.
- Understand wireless discovery and association behavior.
- Investigate suspicious management frames.
- Interpret wireless captures more accurately.

## Key Learnings

- IEEE 802.11 defines Wi-Fi communication.
- Access points provide wireless network access.
- Stations are wireless client devices.
- SSID identifies a network by name.
- BSSID identifies a specific Basic Service Set.
- Channels and frequency bands affect wireless communication.
- Monitor mode enables passive frame capture when the hardware and configuration support it.

---

# Task 3: 802.11 Frames

## Objective

Understand what IEEE 802.11 frames are and how frame types help explain wireless network activity.

## 3.1 What Is an 802.11 Frame?

An IEEE 802.11 frame is a structured unit of information exchanged over a Wi-Fi network.

A frame contains fields that help wireless devices interpret the transmission. Depending on the frame type, these fields can identify the frame's purpose, participating addresses, and other control information.

Wireless packet captures can be used to inspect these frames during authorized network analysis.

## 3.2 Main Types of 802.11 Frames

IEEE 802.11 frames are broadly divided into three major categories.

### A. Management Frames

Management frames help wireless devices discover networks and establish, maintain, or end wireless relationships.

Examples include:

- Beacon
- Probe Request
- Probe Response
- Authentication
- Association Request
- Association Response
- Deauthentication
- Disassociation

**Beacon frames:** Commonly sent by access points to advertise a wireless network and its capabilities.

**Probe Request frames:** Sent by stations to discover suitable wireless networks.

**Probe Response frames:** Sent in response to certain probe requests.

**Authentication and association frames:** Participate in the procedures used to establish a wireless connection.

**Deauthentication frames:** Indicate that an authentication relationship is being terminated.

**Disassociation frames:** Indicate that an association between a station and an access point is being ended.

### B. Control Frames

Control frames help coordinate access to the wireless medium and support the delivery of wireless transmissions.

Examples include:

- RTS (Request to Send)
- CTS (Clear to Send)
- ACK (Acknowledgment)
- Block ACK

These frames help devices coordinate transmissions or acknowledge successful reception at the relevant protocol layer.

### C. Data Frames

Data frames carry data between wireless devices.

Depending on the network configuration and frame subtype, they may carry higher-layer network traffic or other data associated with wireless communication.

When encryption is enabled, a packet capture may not reveal the protected payload in readable form without the appropriate authorized decryption context.

## 3.3 Understanding Wireless Discovery

A typical wireless discovery process can involve:

1. An access point periodically transmits beacon frames.
2. A station scans for available wireless networks.
3. A station may transmit probe requests.
4. An access point may respond with a probe response.
5. The station can proceed through authentication and association procedures if it selects that network.

The exact exchange depends on the network configuration, device behavior, and Wi-Fi security mode.

## 3.4 Understanding Disconnection Activity

Wireless disconnection-related activity can involve deauthentication or disassociation frames.

These frames are not automatically evidence of an attack. They may occur during normal network operations, roaming, troubleshooting, or intentional disconnection.

Repeated or unusual disconnection frames may warrant further investigation when correlated with other evidence.

An analyst should check:

- Source and destination addresses.
- The frame subtype.
- The timestamp and frequency of events.
- Whether the activity affects one station or many.
- Whether the access point and station behavior match the expected environment.
- Whether the capture contains enough information to support a conclusion.

## 3.5 How Frame Analysis Supports an Investigation

Suppose users report repeated Wi-Fi disconnections.

A security analyst may:

1. Obtain an authorized wireless packet capture.
2. Identify the relevant access point and client station.
3. Filter for management frames associated with the affected devices.
4. Examine deauthentication and disassociation events.
5. Compare timestamps with the reported outage.
6. Check whether similar events affect other clients.
7. Document evidence and distinguish confirmed observations from possible explanations.

A capture showing disconnection frames alone does not necessarily establish who initiated an attack or prove malicious intent. Additional evidence may be required.

## 3.6 Important Limitations

- A wireless adapter may not capture all frames.
- A capture on the wrong channel may miss relevant traffic.
- Encryption can prevent direct inspection of protected payloads.
- Some frame fields may be spoofed or misleading.
- A single packet should not be treated as conclusive proof of compromise.

## Key Learnings

- 802.11 frames are the building blocks of Wi-Fi communication.
- Management frames support discovery and connection management.
- Control frames help coordinate wireless transmissions.
- Data frames carry data between wireless devices.
- Deauthentication and disassociation frames can be relevant to outage investigations.
- Frame analysis requires context and correlation before drawing security conclusions.

---

# Overall Summary

The first three tasks introduce the foundations of wireless network security:

1. **Task 1 — Introduction:** Understand the importance of Wi-Fi security and wireless traffic analysis.
2. **Task 2 — How Wi-Fi Works:** Understand IEEE 802.11, access points, stations, SSID, BSSID, BSS, frequency bands, channels, and monitor mode.
3. **Task 3 — 802.11 Frames:** Understand management, control, and data frames, including how discovery and disconnection activity can be analyzed.

These concepts form a foundation for further study of wireless reconnaissance, packet analysis, and authorized wireless security testing.

## Disclaimer

This repository is for educational purposes. All testing and packet capture activities must be performed in authorized lab environments or on networks for which explicit permission has been granted.

