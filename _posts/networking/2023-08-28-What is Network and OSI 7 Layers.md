---
title: "What is Network and OSI 7Layers"
excerpt: "본문의 주요 내용을 여기에 입력하세요"

categories:
  - Networking
tags:
  - [Network, OSI 7layers]

permalink: /networking/post-1/

toc: true
toc_sticky: true

date: 2023-08-28
last_modified_at: 2023-08-28
---

## **Network and Networking: An Overview**
- **`Network`** refers to a group of interconnected devices (such as computers, phones, and servers) that can share data with each other

- **`Networking`** is the process of connecting these devices using hardware and software to facilitate communication. Networks allow data to be exchanged locally (within a single office) or globally (across the internet).

<br>

## **OSI (Open System Interconnection) 7 Layers**
- **`OSI model`** is a conceptual framework that describes how data is transmitted over a network.<br>
It divides the networking process into seven distinct layers, each with its own specific tasks.

<br>

## **Example: Sending a Whatsapp Emoji (😀) from Computer A to B**

- Intra: 내부(인트라넷), Inter: 가로지르는 외부

### **Layer 7: Application Layer**
>This is where applications like **Whatsapp** or **Facebook Messenger** work. In this case, your emoji (😀) is the data being sent. The application layer deals with user-facing processes like messaging, file transfer, and email.<br>
**\* In simple terms:** The app (like Whatsapp) decides what data needs to be sent.

<br>

### **Layer 6: Presentation Layer**
>This layer ensures the data is in the correct format for transmission.The data (😀) is converted into a format that can be sent over the network. For example, it defines the format of the emoticon (e.g., jpg or png). This layer ensures that different devices understand the data format, and it can also handle encryption (scrambling the data for security) and data compression.<br>
**\* In simple terms:** This layer ensures that the format is understood by both the sender and receiver.

<br>

### **Layer 5: Session Layer**
>The session layer manages and maintains communication between devices. It ensures that a session is open and can transfer data(😀) back and forth. This is where the conversation between application entities happens.<br>
**\* In simple terms:** This layer keeps track of the conversation and ensures that data can flow back and forth.

<br>

### **Layer 4: Transport Layer**
>The transport layer determines how data is sent over the network, including whether to use TCP (for reliable transmission) or UDP (for faster but less reliable transmission).<br>
The transport layer adds **port numbers**, which are like apartment numbers in an address that tell the data exactly where it should go on the receiving device.<br>
**\* In simple terms:** This layer decides how the data is sent and ensures it arrives correctly.

- **TCP (Transmission Control Protocol):** Ensures data is delivered correctly and in order, used for tasks like logging in to a website (port 22 for SSH or port 80 for HTTP).<br>
- **UDP (User Datagram Protocol):** This is faster, but less reliable. It's often used for things like streaming videos like YouTube where speed is more important than perfect accuracy. (e.g., DHCP ports 67 and 68).

<br>

### **Layer 3: Network Layer**
>The network layer figures out where to send the data by working with **IP addresses**. Devices like **routers** operate here, deciding the best path for the data to travel across the network.<br>
**\* In simple terms:** This layer determines the address (IP) of the sender and receiver and finds the best route to send the data.

<br>

### **Layer 2: Data Link Layer**
>This layer handles the physical transmission of data over the network, using **MAC addresses (physical hardware addresses)**. Mac address is unique identifies assigned to each device (like an Ethernet care or Wi-Fi adapter). Devices like **switches** operate at this layer, ensuring the data is sent directly from one device to another on the same local network.<br>
**\* In simple terms:** This layer handles the actual connection between devices on a local network, using physical addresses.

<br>

### **Layer 1: Physical Layer**
>The physical layer handles the actual physical transmission of data. It includes hardware like Ethernet cables, fiber optic cables, and Wi-Fi antennas. It defines how bits of data are physically transmitted over these physical connections.<br>
**\* In simple terms:** This layer is all about the physical stuff — wires, signals, and hardware.

<br>

## **Data Names at Each OSI Layer**
As the data moves through each OSI layer, it’s called something different depending on where it is:

>- Layers 7–5 (Application, Presentation, Session): **Message**
>- Layer 4 (Transport): **Segment**
>- Layer 3 (Network): **Packet**
>- Layer 2 (Data Link): **Frame**
>- Layer 1 (Physical): **Bits**

---

**<예시: 컴퓨터 B가 A로부터 전송을 받은 후>**

- 디캡슐레이션(De-capsulation): 전송 받은 정보를 데이터와 헤더가 분리되는 것, 헤더의 정보를 알기 위해서

**<문제>**

![Untitled](Untitled.png)

- 실선: 랜 케이블
1. PC A → Switch1 지나는 찰나 (랜포트): encapsulation 6번(7계층→1계층)
2. Lan cable → Switch1 넘어가는 경계선: decapsulation 1번 (bit→frame) 맥주소 정보 확인
3. Switch1 → Lan cable 경계선: encapsulation 1번 (frame→bit로) *이유: lan cable로 보내야 하기 때문에
4. Lan cable → Router1 경계선: decapsulation 2번 packet 정보 확인 → 출발지/목적지 IP확인
5. Router1 → Lan cable 경계선: encapsulation 2번 (packet을 bit로)

## **TCP/IP 4계층**

- 5계층(Application): 기존 7계층의 7-5계층을 합침
- 4계층(Transport)
- 3계층(Internet)
- 2계층(Link=Network Interface): 기존 7계층의 1-2계층 합침

## **IP(Internet Protocol)**

- IPv4: 업데이트 4번됨
- 처음 미국에서 군사적인 목적으로 통신을 하기위해 만들어짐, 처음부터 국제표준이 될지 몰랐음
- 4개의 옥텟(Octet)으로 구성됨 __.__.__.__
- 하나의 옥텟마다 8bit로 구성됨 (문어다리) *8bit: 0~255($2^8$-1)
- 4개의 옥텟 = **총 32bit (42억개의 IP주소)**
IP범위: 0.0.0.0 ~ 255.255.255.255
- 서브넷 마스크: 네트워크 규모 결정
- 기본 게이트웨이: 다른 웹사이트(외부)와 통신할 때 어느곳으로 나가야 할지에 대한 정보 / 네트워크에서 빠져나가는 가장 빠른 문
- 5클래스 (**A,B,C**,D,E)
    - 주로 쓰이는건 A,B,C 클래스
    - D,E는 연구용 및 브로드캐스트 목적으로 쓰임

## 네트워크 ID / 호스트 ID

- Network ID: 네트워크 식별
- Host ID: 호스트 식별
- 호스트: IP를 갖는 무언가
    - 라우터: 호스트O
    - 스위치: 호스트 X

## **5클래스**

- IP의 규모가 이미 정해져있음
- A클래스
    - 첫 옥텟의 앞자리가 `0`으로 고정됨: 0_ _ _ _ _ _ _ . __ . __ . __
    - 최소/최대값: 0~127($2^7$-1)
    - IP범위: 0.0.0.0~**127**.255.255.255
    - ex. 127.0.0.1
    - 같은 네트워크망에 있으려면 `첫번째` 옥텟이 같아야 함
    - Network ID(첫 옥텟): 네트워크를 나누는데 쓴다, 고정이 되어야 같은 풒 존재한다고 봄
          (노랑: network ID, 초록: host ID)
        - 0.0.0.0 / 0.255.255.255는 같은 네트워크망에 존재
        - 0.0.0.0 / 1.0.0.0은 같은 네트워크망에 존재X
    - 128개의 네트워크가 존재 (0~127)
    - 각 네트워크마다 $2^{24}$의 아이피를 갖을 수 있음 = 규모
    - 총 $2^{24}$ x $2^7$(127)개 = A클래스의 아이패 개수 = $2^{31}$개
    - **클래스풀**(규칙을 따르는것 ↔ 클래스리스)
    
- B클래스
    - 첫 옥텟의 앞자리가 `10`으로 고정됨: 10_ _ _ _ _ _ . __ . __ . __
    - 최소/최대값: 128~191
    - IP범위: 128.0.0.0~**191**.255.255.255
    - 같은 네트워크망에 있으려면 `첫번째, 두번째` 옥텟이 같아야 함
    - 네트워크 구분
        - 128.0.0.0 ~ 128.0.255.255
        - 128.1.0.0 ~ 128.1.255.255
        - …
        - 191.255.0.0 ~ 191.255.255.255
            
            => 총 64x256 = $2^{14}$ 개의 네트워크 존재
            
    - 규모 = $2^{16}$ = 65536개의 아이피 / 한 네트워크 당 (낭비가 심함)
    
- C클래스
    - 첫 옥텟의 앞자리가 `110`으로 고정됨: 110_ _ _ _ _ . __ . __ . __
    - 최소/최대값: 192~223
    - IP범위: **192**.0.0.0~**223**.255.255.255
    - 같은 네트워크망에 있으려면 `첫번째, 두번째, 세번째` 옥텟이 같아야 함
    - 네트워크 구분
        - 192.0.0.0 ~ 192.0.0.255 (하나의 네트워크 당 256개의 아이피)
        - 192.0.1.0 ~ 192.0.1.255 (256개)
        - …
        - 223.255.255.0 ~ 223.255.255.255 (256=$2^8$개)
            
            => 32x256x256 = $2^{21}$개의 네트워크
            
    - 규모 = $2^{8}$
