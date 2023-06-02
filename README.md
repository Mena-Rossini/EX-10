# EX-10 APPLICATION USING TCP SOCKETS - FILE TRANSFER PROGRAM

## DATE : 08-05-2023

## AIM :
To write a python program for creating File Transfer using TCP Sockets Links.

## ALGORITHM :
1. Start the program.
2. Get the frame size from the user.
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server, it will send ACK signal to client otherwise it
will sendNACK signal to client.
6. Stop the program

## PROGRAM :
### CLIENT :
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
### SERVER :
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
    filename = 'myfile.txt'  # Replace 'path/to' with the actual path to the file
    try:
        with open(filename, 'rb') as f:
            l = f.read(1024)
            while l:
                conn.send(l)
                print('Sent', repr(l))
                l = f.read(1024)
        print('Done sending')
    except FileNotFoundError:
        print(f'File {filename} not found.')
    
    conn.send('Thank you for connecting'.encode())
    conn.close()

```
## OUTPUT :
### CLIENT :
![241381436-67e1dfc1-8caa-49ab-8a2d-650c47f0209a](https://github.com/Mena-Rossini/EX-10/assets/102855266/153be27d-3be9-4b4f-8e88-dea96277a263)

### SERVER :

![241381447-f0ca74f3-d3d0-409e-a0cc-67d1a2dcd4de](https://github.com/Mena-Rossini/EX-10/assets/102855266/69a8f9dd-a5cc-4443-9633-e99edb36042d)

## RESULT :
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed .



