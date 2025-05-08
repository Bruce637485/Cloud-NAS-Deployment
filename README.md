# ☁️ Cloud NAS Deployment using MeLE Quieter3C and Python Flask

## 📌 Project Overview

This project demonstrates the deployment of a **Cloud-based Network Attached Storage (NAS)** system using a **MeLE Quieter3C Fanless Mini PC** running **Windows 11**. It enables **secure file sharing over the internet** using **SMB 2.0** and **HTTPS**, with a strong focus on encryption and self-hosted security practices.

---

## 🧠 Key Features

- 🔐 **Secure SMB 2.0 File Sharing**  
  Configured on Windows 11 to allow local network access with permission-based sharing.

- 🌐 **Python Flask Web Interface**  
  Built a custom HTTPS web server using Flask to allow remote access via browser.

- 🧾 **SSL Certificate and BitLocker Encryption**  
  - Self-signed certificate integrated with Flask server for encrypted traffic.
  - BitLocker drive encryption enabled to protect data at rest.

- 🚫 **No Third-Party Services**  
  Designed without reliance on cloud providers like Dropbox, Tailscale, or Google Drive.

---

## 🖥️ System Requirements

- **Hardware**: MeLE Quieter3C Fanless Mini PC  
- **OS**: Windows 11 (Pro or Enterprise preferred for BitLocker)  
- **Dependencies**:
  - Python 3.x
  - Flask
  - OpenSSL (for certificate generation)
  - SMB 2.0 file sharing enabled

---

## 🛠️ Setup Instructions

### 🔧 1. Configure Windows File Sharing

- Enable **SMB 2.0**:
  - `Control Panel > Programs > Turn Windows Features On/Off > SMB 1.0/CIFS File Sharing Support (disable 1.0, ensure 2.0+ is active by default)`
- Share the desired folder with specific user permissions.

### 🔑 2. Enable BitLocker Encryption

- Open `Control Panel > BitLocker Drive Encryption`
- Turn on BitLocker for the data drive used for NAS storage.

### 🐍 3. Install Python and Flask

```bash
pip install flask
```

### 🔐 4. Generate SSL Certificate
```
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365 -nodes
```

### 🧠 5. Python Flask Web Server
```
from flask import Flask, send_from_directory
import os

app = Flask(__name__)

# Serve files from NAS shared directory
@app.route('/files/<path:filename>')
def serve_file(filename):
    shared_dir = "C:/Users/YourUsername/SharedFolder"
    return send_from_directory(shared_dir, filename)

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=443, ssl_context=('cert.pem', 'key.pem'))
```

### 🌍 Remote Access (Optional Advanced Step)
To make this accessible outside your local network:
1. Set a DHCP Reservation for your NAS in your router.
2. Forward port 443 (HTTPS) to your NAS IP address.
3. Optionally, use a dynamic DNS solution if you don't have a static IP.

### 📈 Learning Objectives
- Hands-on implementation of a secure NAS environment
- Application of encryption standards (BitLocker, HTTPS)
- Practical experience with Flask and OpenSSL
- Network service configuration and remote access management

### 🧑‍💻 Author
Bruce R Weygandt
Cybersecurity Undergraduate @ Brigham Young University
🔗 [LinkedIn](https://www.linkedin.com/in/bruce-weygandt)
