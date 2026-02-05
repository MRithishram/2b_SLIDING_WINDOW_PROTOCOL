# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM:
To implement a program to illustrate the mechanism of sliding window protocol
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM:
server.py
```
import socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server listening...")
conn, addr = s.accept()
print(f"Connected to {addr}")

while True:
    frames = conn.recv(1024).decode()
    if not frames:
        break

    print(f"Received frames: {frames}")
    ack_message = f"ACK for frames: {frames}"
    conn.send(ack_message.encode())

conn.close()  
s.close()
```
client.py
```
import socket
c = socket.socket()
c.connect(('localhost', 9999))
size = int(input("Enter number of frames to send: "))
l = list(range(size))  
print("Total frames to send:", len(l))
s = int(input("Enter Window Size: "))
i = 0
while True:
    while i < len(l):
        st = i + s
        frames_to_send = l[i:st]  
        print(f"Sending frames: {frames_to_send}")
        c.send(str(frames_to_send).encode())  
        ack = c.recv(1024).decode()  
        if ack:
            print(f"Acknowledgment received: {ack}")
            i += s  
    break
c.close()  
```
## OUPUT:
<img width="1316" height="249" alt="server" src="https://github.com/user-attachments/assets/188c8c92-c3c4-4fed-9572-2f326368dec4" />
<img width="1324" height="337" alt="client" src="https://github.com/user-attachments/assets/451a1165-5326-428a-a030-52879573b940" />


## RESULT:
Thus, python program to perform stop and wait protocol was successfully executed
