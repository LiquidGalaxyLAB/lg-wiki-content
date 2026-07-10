---
title: How to install npm applications on LG
contributor: Mattia Baggini
date: 2024-06-06T07:41:06.095+00:00
---

## **About** 
\
In this page we will see how install an npm application on Liquid Galaxy \
\
``` ```
***

## **Requirements** 
\
Ensure Node.js version 14 is installed on the master machine by running:
```terminal
node -v
```
\
The output should look like v14.17.5. If not, follow the installation process provided in this tutorial: [How To Install Node.js on Ubuntu 16.04.](https://tecadmin.net/install-latest-nodejs-npm-on-ubuntu/)\
\
After installing Node.js, install pm2 on the master machine. Execute the command:
```terminal
sudo npm i -g pm2
```
Make sure to have configured start.sh and stop.sh following this [guide](https://docs.google.com/document/d/1Jr7MPmuExWNlQc8dDyygTEptZGz7EkIWCCyHK6DoOqE/edit?usp=sharing).\
\
``` ```
***
## **Setup**
\
We must create [one shell executables](https://docs.fileformat.com/programming/sh/) (.sh) file for the installation process.\
\
Let’s start by creating and editing [install.sh.](https://github.com/0xbaggi/scroll_text_application/blob/main/install.sh) First, we need to check if the port and password arguments are provided and then assign the argument values to two variables. At the end, we will define a GAME_FOLDER variable that contains the name of the folder where our Node.js application is located.\
\
Ensure that the start.sh and stop.sh script files are in the same directory as install.sh.
```terminal
if [ "$#" -ne 2 ]; then
    echo "Usage: $0 <port> <sudo_password>"
    exit 1
fi

PORT=$1
PW=$2
GAME_FOLDER="server"

time=$(date +%H:%M:%S)
echo "[$time] Installing application..."
```
\
Now, we need to open the port for our service.
```terminal
LINE=`cat /etc/iptables.conf | grep "tcp" | grep "8111" | awk -F " -j" '{print $1}'`
RESULT=$LINE",$PORT"

DATA=`cat /etc/iptables.conf | grep "tcp" | grep "8111" | grep "$PORT"`

if [ "$DATA" == "" ]; then
  time=$(date +%H:%M:%S)
  echo "[$time] Opening port $PORT..."
  echo $PW | sudo -S sed -i "s/$LINE/$RESULT/g" /etc/iptables.conf
else
  time=$(date +%H:%M:%S)
  echo "[$time] Port already open."
fi
```
\
And finally, we can install our application using the npm install command. We will also add execute permissions for the open.sh and close.sh files.
```terminal
time=$(date +%H:%M:%S)
echo "[$time] Installing dependencies..."
cd $GAME_FOLDER/
echo $PW | sudo -S npm install -y
chmod +x open.sh close.sh

echo $PW | sudo -S chown lg:lg /home/lg/.pm2/rpc.sock /home/lg/.pm2/pub.sock
```
\
Now, we can reboot the service.
```terminal
echo $PW | sudo -S pm2 delete SCROLL_TEXT:$PORT 2> /dev/null

time=$(date +%H:%M:%S)
echo "[$time] Starting pm2..."
echo $PW | sudo -S pm2 start index.js --name SCROLL_TEXT:$PORT
echo $PW | sudo -S pm2 save
```
\
We also want to open the service on startup.
```terminal
time=$(date +%H:%M:%S)
echo "[$time] Updating resurrect script..."
RESURRECT=$(pm2 startup | grep 'sudo')
echo $PW | sudo -S eval $RESURRECT
```
\
And finally, let’s reboot the master.
```terminal
time=$(date +%H:%M:%S)
echo "[$time] Installation complete. Reboot your machine to finish it."
echo $PW | sudo -S reboot
```
\
``` ```
***
## **Usage**
\
Now we have our install script ready to be used. To run a .sh file we must use bash command from terminal like this:
```terminal
bash install.sh <port> <sudo_password>
```
\
Where <port> is the port of your service page and <password> is the liquid galaxy sudo password.\
\
Here is an example of application that implements this logic: [scroll text application](https://github.com/0xbaggi/scroll_text_application)\
\
***That’s all!*** \
written by Mattia Baggini




