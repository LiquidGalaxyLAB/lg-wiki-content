---
title: Configure Flask Server to Be Accessed from Liquid Galaxy Nodes
contributor: Taha Sadikot
date: January 15, 2025
---

---

## The Core Configuration Logic

To ensure the Flask server is accessible to Liquid Galaxy nodes, the following logic is used in your Flask app:

```python
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000)
```

# Explanation  

- `host='0.0.0.0'`: This makes the Flask server listen on all available network interfaces, allowing devices on the same network to access it.  
- `port=8000`: Specifies the port number on which the Flask server will run. Ensure that this port is open on the machine's firewall.  

---

# Steps to Configure the Flask Server  

## Install Flask  
First, ensure Flask is installed on your Python environment:
```bash
pip install flask
```

## Create the Flask App
Write the following Flask app code and save it as `app.py`:
```bash
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/status', methods=['GET'])
def status():
    return jsonify({"message": "Flask server is running and accessible"})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000)
```
## Run the Flask Server
Start the Flask server:
```bash
python app.py
```
The server will now listen on all network interfaces at port `8000`.

## Find Your Local IP Address
On the machine running the Flask server, find its local IP address. Use the following command:
```bash
ip addr show
```
Note the IP address of the network interface connected to the Liquid Galaxy nodes `(e.g., 192.168.1.100)`.

---
# Curl Command to Access the Flask Server from Nodes
To verify connectivity from a Liquid Galaxy node, use the following `curl` command:
```bash
curl http://192.168.1.100:8000/status
```

Replace `192.168.1.100` with the actual IP address of the Flask server.

if everything goes well you will see response from flask server on command prompt.




