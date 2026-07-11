---
title: Chromium on Liquid Galaxy
contributor: Mattia Baggini
date: March 18, 2024
---



## Welcome to our guide on seamlessly managing Chromium on Liquid Galaxy, effortlessly directing it to your desired service page. 

### **Requirements**

First, let’s ensure Chromium is installed on every machine (master and slaves):

```bash
sudo apt-get install chromium-browser
```
or with snap:
```bash
sudo snap install chromium
```

**Setup**

Now, let’s create two sleek shell executables (.sh) files: `open.sh` and `close.sh`.

In `open.sh`, we’ll start by checking and assigning necessary arguments:

```bash
if [ "$#" -ne 2 ]; then									
    echo "Usage: $0 <port> <sudo_password>"					
    exit 1											
fi												
PORT=$1											
PW=$2												
export DISPLAY=:0.0
```

Next, we’ll command Chromium to open in full screen to the specified page and port, without flooding the console with logs:

```bash
chromium-browser --start-fullscreen http://localhost:$PORT > /dev/null 2>&1 &
sleep 1
```

To ensure Chromium opens on all the slaves, we’ll convert the `LG_FRAMES` variable to an array and sort it based on screen number:

```bash
. ${HOME}/etc/shell.conf
lg_frames_array=($LG_FRAMES)
IFS=$'\n' lg_frames_sorted=($(sort -t 'g' -k2n <<<"${lg_frames_array[*]}"))
unset IFS
```

Finally, we’ll iterate over the sorted array and execute start commands:

```bash
for lg in "${lg_frames_sorted[@]}"; do
  screenNumber=${lg:2}
  if [ "$lg" != "lg1" ]; then
    echo $lg
    sshpass -p $PW ssh -tXn $lg "export DISPLAY=:0; chromium-browser http://lg1:$PORT --start-fullscreen &" &
  fi
  sleep 1
done
```

With `open.sh` configured, let’s save the file and proceed to `close.sh`.

Similar to `open.sh`, we’ll ensure the password argument is provided and then iterate over the list of frames to execute the stop command:

```bash
if [ -z "$1" ]; then
    echo "Error: No password provided."
    echo "Usage: $0 <password>"
    exit 1
fi
PW="$1"

. ${HOME}/etc/shell.conf
for lg in $LG_FRAMES; do
  if [ $lg != "lg1" ]; then
    sshpass -p $PW ssh -n $lg "export DISPLAY=:0; pkill chromium-browse; pkill chrome" &
  fi
done
```

Finally, we’ll terminate Chromium processes on the master:

```bash
export DISPLAY=:0
pkill chromium-browse
pkill chrome
```

**Usage**

Your scripts are now primed for action. Simply run a .sh file using the bash command from the terminal:

For opening:
```bash
bash open.sh <port> <password>
```
And for closing:
```bash
bash close.sh <password>
```

Here, `<port>` refers to your service page's port, and `<password>` is the Liquid Galaxy sudo password. Execute these commands via SSH or integrate them into your Flutter application.

**Additional Resources**

For an application example implementing this logic, check out the Scroll Text Application.



