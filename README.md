# CN


# Write a program to implement the STOP AND WAIT PROTOCOL
### SERVER
```
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
while True:
    ip=input("Enter the data : ")
    c.send(ip.encode())
    ack=c.recv(1024).decode()
    if ack:
        print(ack)
        continue
    else:
        c.close()
        break

```
### CLIENT
```
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    print(s.recv(1024).decode())
    s.send("Acknowledgement Received".encode())
```
# Write a program to implement the PING COMMAND
### SERVER
```
import socket
from pythonping import ping
s=socket.socket()
s.bind(('localhost',8001))
s.listen(5)
c,addr=s.accept()
while True:
    hostname=c.recv(1024).decode()
    try:
        c.send(str(ping(hostname,verbose=False)).encode())
    except KeyError:
        c.send("Not Found".encode())
```
### CLIENT
```
import socket
s=socket.socket()
s.connect(('localhost',8001))
while True:
    ip=input("Enter the website yo want to ping : ")
    s.send(ip.encode())
    print(s.recv(1024).decode())
```

# -------------------------------------------------------------
# Write a program to implement the SLIDING WINDOW PROTOCOL
### SERVER
```
import socket
s=socket.socket()
s.bind(('localhost',8002))
s.listen(5)
c,addr=s.accept()
n=int(input("Enter the number of frames to be sent : "))
l=list(range(n))
size=int(input("Enter the Window Size : "))
st=0
i=0
while True:
    while i<len(l):
        st+=size
        c.send(str(l[i:st]).encode())
        ack=c.recv(1024).decode()
        if ack:
            print(ack)
            i+=size
```
### CLIENT
```
import socket
s=socket.socket()
s.connect(('localhost',8002))
while True:
    print(s.recv(1024).decode())
    s.send("Acknowledgement Received".encode())
```
# Write a program to implement the TRACEROUTE COMMAND
```
from scapy.all import*
target=[www.google.com]
result,unans=traceroute(target,maxttl=32)
print(result,unans)
```
# -------------------------------------------------------------
# Write a program to implement the ECHO CLIENT-SERVER APPLICATION USING TCP SOCKETS 
### SERVER
```
import socket
s=socket.socket()
s.bind(('localhost',8004))
s.listen(5)
c,addr=s.accept()
while True:
    ClientMessage=c.recv(1024).decode()
    c.send(ClientMessage.encode())
```
### CLIENT
```
import socket
s=socket.socket()
s.connect(('localhost',8004))
while True:
    ip=input("Client - > ")
    s.send(ip.encode())
    print("Server - > ",s.recv(1024).decode())
```
# Write a program to implement the ADDRESS RESOLUTION PROTOCOL (ARP)
### SERVER
```
import socket
s=socket.socket()
s.bind(('localhost',8005))
s.listen(5)
c,addr=s.accept()
address={'165.165.80.80':'8A:6C:07:EF','165.165.01.79':'AA:BB:CF:ED'}
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```
### CLIENT
```
import socket
s=socket.socket()
s.connect(('localhost',8005))
while True:
    ip=input("Enter logical address : ")
    s.send(ip.encode())
    print("Mac Address : ",s.recv(1024).decode())
```
# -------------------------------------------------------------
# Write a program to implement the CHAT APPLICATION USING TCP SOCKETS 
### SERVER
```
import socket
s=socket.socket()
s.bind(('localhost',8007))
s.listen(5)
c,addr=s.accept()
while True:
    ClientMessage=c.recv(1024).decode()
    print("Client - > ",ClientMessage)
    msg=input("Server - > ")
    c.send(msg.encode())
```
### CLIENT
```
import socket
s=socket.socket()
s.connect(('localhost',8007))
while True:
    ip=input("Client - > ")
    s.send(ip.encode())
    print("Server - > ",s.recv(1024).decode())
```
# Write a program to implement the REVERSE ADDRESS RESOLUTON PROTOCOL (RARP)
### SERVER
```
import socket
s=socket.socket()
s.bind(('localhost',8006))
s.listen(5)
c,addr=s.accept()
address={'8A:6C:07:EF':'195.195.60.60','AA:BB:CF:ED':'192.192.79.01'}
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```
### CLIENT
```
import socket
s=socket.socket()
s.connect(('localhost',8006))
while True:
    ip=input("Enter Mac Address : ")
    s.send(ip.encode())
    print("Logical Address : ",s.recv(1024).decode())
```
# -------------------------------------------------------------
# Write a program to implement the FILE TRANSFER APPLICATION USING TCP SOCKETS
### TEXT FILE
```
RANDON TEXT
```
### SERVER
```
import socket 
port = 60000 
s = socket.socket() 
host = socket.gethostname() 
s.bind((host, port)) 
s.listen(5) 
while True:
    conn, addr = s.accept() 
    data = conn.recv(1024)
    print('Server received', repr(data))
    filename='mytext.txt'
    f = open(filename,'rb')
    l = f.read(1024)
    while (l):
        conn.send(l)
        print('Sent ',repr(l))
        l = f.read(1024)
    f.close()
    print('Done sending')
    conn.send('Thank you for connecting'.encode())
    conn.close()
```
### CLIENT
```
import socket
s = socket.socket()
host = socket.gethostname()
port = 60000
s.connect((host, port))
s.send("Hello server!".encode())
with open('received_file', 'wb') as f:
    while True:
        print('receiving data...')
        data = s.recv(1024)
        print('data=%s', (data))
        if not data:
            break
        f.write(data)
f.close()
print('Successfully get the file')
s.close()
print('connection closed')

```
# Write a program to perform SOCKET PROGRAMMING with CLIENT-SERVER MODEL
### SERVER
```
import socket
from datetime import datetime
s=socket.socket()
s.bind(('localhost',8008))
s.listen(5)
c,addr=s.accept()
print("Address : ",addr)
now=datetime.now()
c.send(now.strftime('%d/%m/%Y %H:%M:%S').encode())
ack=c.recv(1024).decode()
if ack:
    print (ack)
c.close()
```
### CLIENT
```
import socket
s=socket.socket()
s.connect(('localhost',8008))
print(s.getsockname())
print(s.recv(1024).decode())
print("Acknowledgemnet Received".encode())
```
