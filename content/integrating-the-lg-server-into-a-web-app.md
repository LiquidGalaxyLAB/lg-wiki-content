---
title: Integrating the LG Server into a Web App
contributor: Karan Kumar Das
date: 2025-04-11T18:36:09.060+00:00
---

# Integrating the LG Server into a Web App
## Introduction
The **LG server** is a Node.js-based control server designed to manage and control Liquid Galaxy rigs via SSH. This guide details the process of connecting Liquid Galaxy rigs with your web application using the LG server. You’ll learn about its REST API endpoints, project structure, and how to extend its functionalities to execute various commands on your Liquid Galaxy Rigs.

Here is the official Github repository link of the lg-sever : https://github.com/LiquidGalaxyLAB/lg-server

Here is the link to the lg-server Swagger API documentation: : https://rohit-554.github.io/LgServerSwaggerApi/#/

To integrate the LG server into your web application, ensure you have the following prerequisites:
- Ensure that Node.js is installed on your system to run the LG Server.
- Verify that your Liquid Galaxy rig is correctly set up on your device.
- Have familiarity with RESTful APIs to facilitate communication with the LG Server.
- Set up a development environment using tools such as Node.js, Vite, or React.
# Starting the LG Server Locally
### 1. Clone the Repository

```bash
git clone https://github.com/LiquidGalaxyLAB/lg-server.git
cd lg-server
```
### 2. Install Dependencies :

```bash
npm install
```
### 3. Start the LG Server :

```bash
npm run dev
```
### 4. Verify the server is running : 


```bash
curl http://localhost:3000/ping
```
Expected Message : { "message": "pong@@" }
## Connecting your Web App to the LG Rigs

The LG Server exposes several RESTful endpoints that can be used to send commands to the Liquid Galaxy rigs. Before executing any commands, we need to establish a connection with the LG rig.
### 1. Establishing Connection with Liquid Galaxy
```javascript
const connectToLG = async (ip, port, username, password) => {
    try {
        const response = await fetch('http://localhost:3000/api/lg-connection/connect-lg', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ ip, port, username, password })
        });

        const data = await response.json();
        console.log('Connected to LG:', data);
    } catch (error) {
        console.error('Error connecting to LG:', error);
    }
};
```
### 2. Verifying Connection with Liquid Galaxy
```javascript
const checkLGConnection = async (ip, port, username, password) => {
    try {
        const response = await fetch('http://localhost:3000/api/lg-connection/check-connection', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ ip, port, username, password })
        });

        const data = await response.json();
        console.log('LG Connection Status:', data);
    } catch (error) {
        console.error('Error checking LG connection:', error);
    }
};
```
### 3. Executing Flyto Command After Successful Connection

```javascript
export const flyto = async (
    ip, port, username, password, numberOfRigs, latitude, longitude, 
    elevation, tilt, bearing
) => {
    try {
        const response = await fetch('http://localhost:3000/api/lg-connection/flyto', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({
                ip, port, username, password, screens: numberOfRigs, 
                latitude, longitude, elevation, tilt, bearing,
            }),
        });

        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Error:', error);
    }
};
```
You can explore other API endpoints from the Swagger documentation, where you'll find detailed information about the API request body and response structure.

If you want to deploy your frontend application and make API calls to a remote LG Server, follow the setup guide provided in the LG Server repository's README.

You can take a look at this [GitHub repository](https://github.com/karankoder/liquid-galaxy-presentation), where I have integrated the LG Server into my web application for demonstration purposes.

Additionally, you can watch the [streaming series video](https://www.youtube.com/watch?v=9BFrK2WoCUY&t=1765s), where I have recorded the full process step by step. These resources will help you understand the integration and execution workflow in detail.
## Conclusion
By integrating the LG Server using RESTful APIs, you can remotely control Liquid Galaxy operations from your web application. The endpoints allow you to execute orbits, relaunch LG, clean visualizations, and run custom SSH commands, making it a powerful tool for managing Liquid Galaxy systems through a web interface.



