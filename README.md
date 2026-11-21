# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM:
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
### server program:
```
import socket

s = socket.socket()
s.bind(('localhost', 12345))
s.listen(1)

print("Server is waiting for client...")

c, addr = s.accept()
print("Client connected")

arp_table = {
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02",
    "192.168.1.3": "AA:BB:CC:DD:EE:03"
}

ip = c.recv(1024).decode()
print("Received IP:", ip)

mac = arp_table.get(ip, "IP Address not found")

c.send(mac.encode())

c.close()
s.close()
```
### client program:
```
import socket

s = socket.socket()
s.connect(('localhost', 12345))

ip = input("Enter IP address: ")

s.send(ip.encode())

mac = s.recv(1024).decode()

print("MAC Address:", mac)

s.close()

```
## OUPUT - ARP
<img width="1917" height="1006" alt="image" src="https://github.com/user-attachments/assets/85e49333-c01d-4f5a-934f-6ba184147968" />
<img width="1917" height="1017" alt="image" src="https://github.com/user-attachments/assets/9dfcb6cb-3694-4eca-8f2d-e545e113c36f" />

## PROGRAM - RARP
### server program:
```

import socket

s = socket.socket()
s.bind(('localhost', 12346))
s.listen(1)

print("RARP Server waiting...")

c, addr = s.accept()

rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}

mac = c.recv(1024).decode()

ip = rarp_table.get(mac, "MAC not found")

c.send(ip.encode())

print("MAC Address:", mac)
print("IP Address:", ip)

c.close()
s.close()

```
### client program:
```

import socket

s = socket.socket()
s.connect(('localhost', 12346))

mac = input("Enter MAC Address: ")

s.send(mac.encode())

ip = s.recv(1024).decode()

print("IP Address:", ip)

s.close()

```
## OUPUT -RARP
<img width="1917" height="1015" alt="Screenshot 2026-11-21 082100" src="https://github.com/user-attachments/assets/bbf094aa-0cf7-4369-8bbc-8401ef2805da" />
<img width="1917" height="1013" alt="Screenshot 2026-11-21 082119" src="https://github.com/user-attachments/assets/2ad91062-0a82-459c-8ee1-f947206cf99c" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
