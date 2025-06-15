# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
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

ARP_client:
```
import socket
c = socket.socket()
c.connect(('localhost', 8000))

while True:
    ip = input("Enter IP address to find MAC (or type 'exit' to quit): ")

    if ip.lower() == "exit":  
        break

    c.send(ip.encode())
    mac = c.recv(1024).decode()
    print(f"MAC Address for {ip}: {mac}")
c.close()

```

ARP_server:
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")

c, addr = s.accept()
print(f"Connection established with {addr}")

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:  
        break

    print(f"Received IP: {ip}")

    mac = address.get(ip, "MAC address not found")
    c.send(mac.encode())

c.close()
```
## OUPUT - ARP
![Screenshot 2025-03-17 060840](https://github.com/user-attachments/assets/bf0aa743-9a38-42c6-8524-2123e173a950)
![Screenshot 2025-03-17 060828](https://github.com/user-attachments/assets/50c60c7f-5c0c-46a1-8968-98fbbee80931)


## PROGRAM - RARP
RARP_client:
```
import socket
c = socket.socket()
c.connect(('localhost', 8000))

while True:
    mac = input("Enter MAC address to find IP (or type 'exit' to quit): ")
    if mac.lower() == "exit":  
        break
    c.send(mac.encode())
    ip = c.recv(1024).decode()
    print(f"IP Address for {mac}: {ip}")
c.close()
```

RARP_server:
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening for RARP requests...")

c, addr = s.accept()
print(f"Connection established with {addr}")

rarp_table = {
    "6A:08:AA:C2": "165.165.80.80",
    "8A:BC:E3:FA": "165.165.79.1"
}

while True:
    mac = c.recv(1024).decode()
    if not mac:
        break

    print(f"Received MAC: {mac}")
    ip = rarp_table.get(mac, "IP address not found")
    c.send(ip.encode())

c.close()
s.close()

```

## OUPUT -RARP
![Screenshot 2025-03-17 061750](https://github.com/user-attachments/assets/3def4b4c-9aeb-4a64-bfc9-cdb2ca211af6)


![Screenshot 2025-03-17 061807](https://github.com/user-attachments/assets/ed65f70d-e71b-4db8-b6ca-c3e54f0fb989)

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
