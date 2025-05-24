# 🧠 Network Protocol Simulation: ARP & RARP using Python (TCP Sockets)



## 📌 AIM

To simulate the **Address Resolution Protocol (ARP)** and **Reverse Address Resolution Protocol (RARP)** using Python and TCP socket programming.



## ⚙️ REQUIREMENTS

- Python 3.x
- Basic understanding of socket programming
- Two terminal windows (or client/server setup)

---

## 👨‍💻 DEVELOPED BY

#### Name: **Kabelan G K** 
#### Reg No: **212224110027**

## 🔁 ALGORITHMS

### ✅ ARP (Address Resolution Protocol)

**Client:**
1. Start the client script.
2. Connect to the ARP server via TCP.
3. Input the IP address to resolve.
4. Send the IP address to the server.
5. Receive and display the corresponding MAC address.

**Server:**
1. Start the server script.
2. Accept incoming connections from client(s).
3. Maintain a static mapping of IP addresses to MAC addresses.
4. Receive the IP address and return the mapped MAC address or an error message.



### 🔁 RARP (Reverse Address Resolution Protocol)

**Client:**
1. Start the client script.
2. Connect to the RARP server via TCP.
3. Input the MAC address to resolve.
4. Send the MAC address to the server.
5. Receive and display the corresponding IP address.

**Server:**
1. Start the server script.
2. Accept incoming connections from client(s).
3. Maintain a static mapping of MAC addresses to IP addresses.
4. Receive the MAC address and return the mapped IP address or an error message.



## 💻 PROGRAMS

### 🔗 ARP Server (`arp_server.py`)

```python
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("ARP Server is listening on port 8000...")
c, addr = s.accept()

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()
    print(f"Received IP: {ip}")
    mac = address.get(ip, "Not Found")
    c.send(mac.encode())
```



### 🔗 ARP Client (`arp_client.py`)

```python
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter Logical Address (IP): ")
    s.send(ip.encode())
    print("MAC Address:", s.recv(1024).decode())
```



### 🔁 RARP Server (`rarp_server.py`)

```python
import socket

s = socket.socket()
s.bind(('localhost', 8001))
s.listen(5)
print("RARP Server is listening on port 8001...")
c, addr = s.accept()

address = {
    "6A:08:AA:C2": "165.165.80.80",
    "8A:BC:E3:FA": "165.165.79.1"
}

while True:
    mac = c.recv(1024).decode()
    print(f"Received MAC: {mac}")
    ip = address.get(mac, "Not Found")
    c.send(ip.encode())
```



### 🔁 RARP Client (`rarp_client.py`)

```python
import socket

s = socket.socket()
s.connect(('localhost', 8001))

while True:
    mac = input("Enter Physical Address (MAC): ")
    s.send(mac.encode())
    print("IP Address:", s.recv(1024).decode())
```



## ✅ SAMPLE OUTPUT

### ARP

```bash
Client Input:
Enter Logical Address (IP): 165.165.80.80

Server Output:
Received IP: 165.165.80.80

Client Output:
MAC Address: 6A:08:AA:C2
```

### RARP

```bash
Client Input:
Enter Physical Address (MAC): 6A:08:AA:C2

Server Output:
Received MAC: 6A:08:AA:C2

Client Output:
IP Address: 165.165.80.80
```


## 🧪 RESULT

Both **ARP** and **RARP** protocols were successfully simulated using Python TCP socket programming. The client-server architecture correctly resolves logical-to-physical (ARP) and physical-to-logical (RARP) addresses using predefined mappings.



---
