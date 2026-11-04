# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM:
To implement the Sliding Window Protocol using Python socket programming, where multiple frames are transmitted from the client to the server based on the specified window size, and acknowledgements (ACK) are received from the server for successful frame transmission.

## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program

## SERVER CODE 
```

import socket

s = socket.socket()

s.bind(('localhost', 8000))

s.listen(1)

print("Waiting for connection...")

conn, addr = s.accept()

print("Connected to", addr)

while True:
    data = conn.recv(1024).decode()

    if not data:
        break

    print("Frames received:", data)

    ack = "ACK for " + data

    conn.send(ack.encode())

conn.close()
s.close()
```
## OUTPUT
<img width="561" height="163" alt="image" src="https://github.com/user-attachments/assets/f35d79ea-b430-4178-a94f-0c52da377aae" />

## CLIENT CODE
```

import socket

s = socket.socket()

s.connect(('localhost', 8000))

n = int(input("Enter number of frames: "))

w = int(input("Enter window size: "))

frames = list(range(1, n + 1))

i = 0

while i < n:
    send_frames = frames[i:i + w]

    msg = " ".join(map(str, send_frames))

    print("Sending frames:", msg)

    s.send(msg.encode())

    ack = s.recv(1024).decode()

    print("Received:", ack)

    i += w

s.close()
```
## OUTPUT
<img width="568" height="232" alt="image" src="https://github.com/user-attachments/assets/3a31271b-b621-4ed4-95aa-cd43337af8e6" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
