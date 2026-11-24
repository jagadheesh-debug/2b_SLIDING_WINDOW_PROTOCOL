# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
## CLIENT
```

import socket

s = socket.socket()
s.connect(("localhost", 8000))

n = int(input("Enter number of frames: "))
w = int(input("Enter window size: "))

frames = []

for i in range(n):
    data = input("Enter data for frame " + str(i + 1) + ": ")
    frames.append(data)

i = 0

while i < n:
    print("\nSending frames:")

    for j in range(i, min(i + w, n)):
        print("Sending:", frames[j])
        s.send(frames[j].encode())

        ack = s.recv(1024).decode()
        print("Received:", ack)

    i = i + w

s.send("exit".encode())
s.close()

```
## SERVER
```
import socket

s = socket.socket()
s.bind(("localhost", 8000))
s.listen(1)

print("Server waiting for client...")

c, addr = s.accept()
print("Client connected!")

while True:
    data = c.recv(1024).decode()

    if data == "exit":
        break

    print("Received:", data)

    c.send("ACK".encode())
    print("ACK sent")

c.close()
s.close()

```
## OUPUT
## CLIENT
<img width="536" height="410" alt="image" src="https://github.com/user-attachments/assets/b301a359-108d-4593-afa3-a2571ba9638c" />

## SERVER
<img width="490" height="272" alt="image" src="https://github.com/user-attachments/assets/38c80935-55c1-4c5c-8078-6152da1bb9ba" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
