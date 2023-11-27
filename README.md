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

```
### CLIENT
```

```
# Write a program to implement the TRACEROUTE COMMAND
```

```
# -------------------------------------------------------------
# Write a program to implement the ECHO CLIENT-SERVER APPLICATION USING TCP SOCKETS 
### SERVER
```

```
### CLIENT
```

```
# Write a program to implement the ADDRESS RESOLUTION PROTOCOL (ARP)
### SERVER
```

```
### CLIENT
```

```
# -------------------------------------------------------------
# Write a program to implement the CHAT APPLICATION USING TCP SOCKETS 
### SERVER
```

```
### CLIENT
```

```
# Write a program to implement the REVERSE ADDRESS RESOLUTON PROTOCOL (RARP)
### SERVER
```

```
### CLIENT
```

```
# -------------------------------------------------------------
# Write a program to implement the FILE TRANSFER APPLICATION USING TCP SOCKETS
### SERVER
```

```
### CLIENT
```

```
# Write a program to perform SOCKET PROGRAMMING with CLIENT-SERVER MODEL
### SERVER
```

```
### CLIENT
```

```
