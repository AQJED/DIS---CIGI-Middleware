# DIS to CIGI Middleware Project

## Overview
This project is a middleware application that facilitates communication between a **Computer-Generated Forces (CGF) system** and an **Image Generator (IG)** by converting **DIS (Distributed Interactive Simulation) protocol** packets into **CIGI (Common Image Generator Interface) protocol** packets.

## System Architecture
The middleware performs the following tasks:

1. **Capture DIS Packets**  
   - The middleware captures **DIS protocol** packets from the **CGF computer** using **PCAPPLUSPLUS**.
   - The data is extracted from the network using a **Cisco switch**.

2. **Store Data in Shared Memory**  
   - The captured **DIS packets** are written into a **shared memory buffer**.
   - Each packet is marked with a flag to indicate whether it is **ready to be processed**.

3. **Read Data from Shared Memory**  
   - The middleware continuously checks for available packets in **shared memory**.
   - Once a packet is ready, it is retrieved for processing.

4. **Convert DIS to CIGI**  
   - The **DIS packet** is parsed using the **Open DIS** library.
   - Key parameters such as **Entity ID, Position, Orientation, and Appearance** are mapped to **CIGI Entity Control Packets** using the **CIGI CCL** library.

5. **Send CIGI Packets to IG**  
   - The converted **CIGI packets** are sent to the **AECHLON Image Generator (IG)** using **Boost.Asio** for **TCP/UDP communication**.

## Libraries Used
The middleware is developed in **C++** using the following libraries:

1. **PCAPPLUSPLUS** – Capturing network packets from the CGF computer.
2. **Open DIS** – Parsing and interpreting **DIS protocol packets**.
3. **CIGI CCL** – Constructing and managing **CIGI protocol packets**.
4. **Boost** – Shared memory management and network communication.

## Hardware and Software Requirements
- **Hardware:**
  - **CGF Computer** – Generates DIS packets.
  - **Cisco Switch** – Connects the CGF system to the middleware.
  - **AECHLON Image Generator (IG)** – Receives CIGI packets.

- **Software:**
  - **C++ languge only as the Middleware** – No software tools or frameworks are used.

## Key Features
- **Real-time Data Processing**: Ensures smooth conversion of simulation data with minimal latency.
- **Efficient Shared Memory Handling**: Uses **Boost.Interprocess** to manage **DIS packet buffering**.
- **Protocol Mapping**: Converts relevant **DIS EntityStatePDU** parameters into **CIGI Entity Control Packets**.
- **Network Communication**: Sends CIGI packets to the **IG** via **Boost.Asio**.

## Data Flow Diagram

CGF Computer (DIS Packets)  
↓  
PCAPPLUSPLUS (Packet Capture)  
↓  
Shared Memory (Boost)  
↓  
Middleware (DIS to CIGI Conversion)  
↓  
Boost.Asio (CIGI Packet Transmission)  
↓  
AECHLON IG (CIGI Packets Rendered)  

## Conclusion
This middleware **bridges the gap between CGF and IG** by efficiently capturing, processing, and converting **DIS** packets into **CIGI** format. The solution is designed for **real-time simulation environments**, ensuring **accurate entity representation** on the AECHLON IG.
