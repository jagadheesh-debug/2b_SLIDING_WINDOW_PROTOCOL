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

skt = socket.socket()
skt.bind(('localhost', 1234))
skt.listen(5)
print("Waiting for server connection...")
c, addr = skt.accept()

while True:
    try:
        size = int(input("Enter number of frames to send: "))
        if size > 0:
            break
        print("Enter a positive number.")
    except ValueError:
        print("Invalid input! Enter numbers only.")

frames = list(range(size))

while True:
    try:
        window = int(input("Enter Window Size: "))
        if 0 < window <= size:
            break
        print("Enter a valid window size.")
    except ValueError:
        print("Invalid input! Enter numbers only.")

start = 0

while start < len(frames):
    end = min(start + window, len(frames))
    c.send(str(frames[start:end]).encode())
    ack = c.recv(1024).decode()
    if ack:
        print(ack)
    start = end

c.close()
skt.close()
```
## SERVER
```
import socket

s = socket.socket()
s.connect(('localhost', 1234))

while True:
    data = s.recv(1024).decode()

    if not data:
        break

    print("Received frames:", data)
    s.send("Acknowledgement received from the server".encode())

s.close()
```
## OUPUT
## CLIENT
<img width="948" height="325" alt="Screenshot 2026-11-04 090437" src="https://github.com/user-attachments/assets/d24fb4b3-3a30-4a6d-86ba-aff8ce34c33b" />

## SERVER
<img width="690" height="203" alt="Screenshot 2026-11-04 090447" src="https://github.com/user-attachments/assets/a58d4e5a-52dd-4589-b423-5766e6d9f830" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
