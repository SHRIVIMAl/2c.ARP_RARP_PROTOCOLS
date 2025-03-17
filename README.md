# 2c.SIMULATING ARP /RARP PROTOCOLS
NAME:T.K.SHRIVIMAL

REF NO:212224220101

DEPT:IT
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

# SERVER
~~~
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

    try:
        mac = address[ip]  # Get the MAC address for the IP
        print(f"IP: {ip} -> MAC: {mac}")
        c.send(mac.encode())  
    except KeyError:
        print(f"IP: {ip} not found in ARP table.")
        c.send("Not Found".encode())
c.close()
s.close()
~~~

# Client
~~~
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
~~~

## OUPUT - ARP
# SERVER
![Screenshot 2025-03-17 151335](https://github.com/user-attachments/assets/268d3400-22e0-4b79-a0a4-f39b540a67a0)


# Client
![Screenshot 2025-03-17 151347](https://github.com/user-attachments/assets/38e6cf4e-86f9-4759-b548-f1ee71e8d83c)

## PROGRAM - RARP
# SERVER
~~~
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")

c, addr = s.accept()
print(f"Connection established with {addr}")

address = {
     "6A:08:AA:C2":"165.165.80.80",
    "8A:BC:E3:FA" :"165.165.79.1"
}

while True:
    ip = c.recv(1024).decode()

    if not ip:
        break
    try:
        mac = address[ip]
        print(f"IP: {ip} -> MAC: {mac}")
        c.send(mac.encode())
    except KeyError:
        print(f"IP: {ip} not found in ARP table.")
        c.send("Not Found".encode())

c.close()
s.close()
~~~
# Client
~~~
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
~~~
## OUPUT -RARP
SERVER
![Screenshot 2025-03-17 151527](https://github.com/user-attachments/assets/53aace99-6daa-42c5-b7cf-ba15d672f780)

Client
![Screenshot 2025-03-17 151537](https://github.com/user-attachments/assets/c42af7c8-a9aa-436e-8b04-11c8312e877a)

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
