---
title: "#1. Network and OSI 7 Layers"
excerpt: "Network refers to a group of interconnected devices (such as computers, phones, and servers) that can share data with each other. Networking is the process of connecting"

categories:
  - Networking
tags:
  - [Network, OSI 7 Layers, Encapsulation, Decapsulation]

permalink: /networking/post-1-230828/

toc: true
toc_sticky: true

date: 2023-08-28
last_modified_at: 2023-08-28
---

## **Network and Networking: An Overview**
---
- `Network` refers to a group of interconnected devices (such as computers, phones, and servers) that can share data with each other.

- `Networking` is the process of connecting these devices using hardware and software to facilitate communication. Networks allow data to be exchanged locally (within a single office) or globally (across the internet).

<br>

## **OSI (Open System Interconnection) 7 Layers**
---
`OSI model` is a conceptual framework that describes how data is transmitted over a network.<br>
It divides the networking process into seven distinct layers, each with its own specific tasks.

<br>

## **Example) Sending a Whatsapp Emoji (😀) from Computer A to B**
---
<!-- - Intra: 내부(인트라넷), Inter: 가로지르는 외부 -->

### **Layer 7: Application Layer**
> This is where applications like **Whatsapp** or **Facebook Messenger** work. In this case, your emoji (😀) is the data being sent.<br>
The application layer deals with user-facing processes like messaging, file transfer, and email.<br>
**\* In simple terms:** The app (like Whatsapp) decides what data needs to be sent.

<br>

### **Layer 6: Presentation Layer**
>This layer ensures the data is in the correct format for transmission.The data (😀) is converted into a format that can be sent over the network. For example, it defines the format of the emoticon (e.g., jpg or png).<br>
This layer ensures that different devices understand the data format, and it can also handle encryption (scrambling the data for security) and data compression.<br>
**\* In simple terms:** This layer ensures that the format is understood by both the sender and receiver.

<br>

### **Layer 5: Session Layer**
>The session layer manages and maintains communication between devices. It ensures that a session is open and can transfer data(😀) back and forth.<br>
This is where the conversation between application entities happens.<br>
**\* In simple terms:** This layer keeps track of the conversation and ensures that data can flow back and forth.

<br>

### **Layer 4: Transport Layer**
>The transport layer determines how data is sent over the network, including whether to use TCP (for reliable transmission) or UDP (for faster but less reliable transmission).<br>
The transport layer adds **port numbers**, which are like apartment numbers in an address that tell the data exactly where it should go on the receiving device.<br>
**\* In simple terms:** This layer decides how the data is sent and ensures it arrives correctly.

<span style="background-color:#fff5b1">**&nbsp;📌 TCP & UDP&ensp;**</span>

- **TCP (Transmission Control Protocol):** Ensures data is delivered correctly and in order, used for tasks like logging in to a website (port 22 for SSH or port 80 for HTTP).<br>
- **UDP (User Datagram Protocol):** This is faster, but less reliable. It's often used for things like streaming videos like YouTube where speed is more important than perfect accuracy. (e.g., DHCP ports 67 and 68).

<br>

### **Layer 3: Network Layer**
>The network layer figures out where to send the data by working with **IP addresses**.<br>
Devices like **routers** operate here, deciding the best path for the data to travel across the network.<br>
**\* In simple terms:** This layer determines the address (IP) of the sender and receiver and finds the best route to send the data.

<br>

### **Layer 2: Data Link Layer**
>This layer handles the physical transmission of data over the network, using **MAC addresses (physical hardware addresses)**.<br>
Mac address is unique identifies assigned to each device (like an Ethernet care or Wi-Fi adapter).<br>
Devices like **switches** operate at this layer, ensuring the data is sent directly from one device to another on the same local network.<br>
**\* In simple terms:** This layer handles the actual connection between devices on a local network, using physical addresses.

<br>

### **Layer 1: Physical Layer**
>The physical layer handles the actual physical transmission of data.<br>
It includes hardware like Ethernet cables, fiber optic cables, and Wi-Fi antennas.<br>
It defines how bits of data are physically transmitted over these physical connections.<br>
**\* In simple terms:** This layer is all about the physical stuff — wires, signals, and hardware.

<br>

## **Data Names at Each OSI Layer**
---
As the data moves through each OSI layer, it’s called something different depending on where it is:
>- Layers 7–5 (Application, Presentation, Session): **Message/Data**
>- Layer 4 (Transport): **Segment**
>- Layer 3 (Network): **Packet**
>- Layer 2 (Data Link): **Frame**
>- Layer 1 (Physical): **Bits**

<br>

## **Encapsulation and Decapsulation in Networking**
---
<small>[img source_ByteByteGo Newsletter](https://blog.bytebytego.com/p/network-protocols-run-the-internet)</small>
![](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F98d7dda0-c161-4568-80f2-6f06d25eb804_1600x1147.png)

### **What is Encapsulation and how it works?**

`Encapsulation` is the process of **adding headers to data** as it moves through the layers of the network.<br>
Each layer of the **OSI model** wraps the data with specific information to ensure it gets to the right destination.

>✏️ Think of it like putting a letter into an envelope, then adding the sender's and recipient's addresses before mailing it.<br>
The data is wrapped in layers, and each layer serves a purpose.


| **OSI Layer**             | **Function**                                                        |
|---------------------------|---------------------------------------------------------------------|
| **Application Layer (Layer 7)** | The original data (like a message or file) is created by an app.   |
| **Transport Layer (Layer 4)**   | Adds port numbers to help manage communication.                  |
| **Network Layer (Layer 3)**     | Adds IP addresses to route the data to the correct device.        |
| **Data Link Layer (Layer 2)**   | Adds MAC addresses to identify devices on the network.            |
| **Physical Layer (Layer 1)**    | Converts everything into bits for transmission over the network.  |

At each layer, data gets wrapped with a header, forming units like **packets** or **frames**. This is called **encapsulation**.

<br>

### **What is Decapsulation and how it works?**

`Decapsulation` is the reverse of encapsulation. As the data reaches its destination, each layer of the OSI model **removes its header**, revealing the original data.

| **OSI Layer**                 | **Function**                                                    |
|-------------------------------|-----------------------------------------------------------------|
| **Physical Layer (Layer 1)**   | Receives bits over the network.                                 |
| **Data Link Layer (Layer 2)**  | Removes MAC address info.                                       |
| **Network Layer (Layer 3)**    | Strips away the IP address.                                     |
| **Transport Layer (Layer 4)**  | Removes port information.                                       |
| **Application Layer (Layer 7)**| Delivers the original message or file to the app.               |

<br>

### **Why Are Encapsulation and Decapsulation Important?**
- **Ensure data reaches the right destination** by adding addresses and control information.
- **Allow communication** between different devices and networks.
- **Maintain data integrity** by including error-checking details.

👉 In short, **encapsulation** packages data for travel across the network, while **decapsulation** unpacks it once it arrives.
