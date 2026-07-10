---
title: How to open and close Chromium sessions on LG
contributor: Mattia Baggini
date: 2024-06-05T16:06:57.484+00:00
---

## **About**
\
In this page we will see how open and close chromium on Liquid Galaxy to a target page that can be you main page of your service.\
\________________________________________________________________________________________________________________
## **Requirements**
\
First we will need to install chromium on every machine (master and slaves):
```terminal
sudo apt-get install chromium-browser
```
or with snap:
```terminal
sudo snap install chromium
```
\________________________________________________________________________________________________________________
## **Setup**
\
Now we must create two [shell executables](https://docs.fileformat.com/programming/sh/) (.sh) files, [open.sh](https://github.com/0xbaggi/scroll_text_application/blob/main/open.sh) and [close.sh](https://github.com/0xbaggi/scroll_text_application/blob/main/close.sh).
Let’s start by creating and editing open.sh: first we need to check if the port and password arguments are provided and then assign the arguments values at two variable.

```dart
if [ "$#" -ne 2 ]; then									
    echo "Usage: $0 <port> <sudo_password>"					
    exit 1											
fi												
PORT=$1											
PW=$2												
export DISPLAY=:0.0
```
\
Now we can enter the command to open Chromium in full screen to the specified page and port, without printing logs in the console.
```dart
chromium-browser --start-fullscreen http://localhost:$PORT > /dev/null 2>&1 &
sleep 1
```
\
We will need to open chromium also in all the slaves so we need to convert the LG_FRAMES variable to an array (LG_FRAMES indicate the slaves) and we will use a custom sort function to sort the array based on the screen number.
```dart
. ${HOME}/etc/shell.conf
lg_frames_array=($LG_FRAMES)
IFS=$'\n' lg_frames_sorted=($(sort -t 'g' -k2n <<<"${lg_frames_array[*]}"))
unset IFS
```
\
Now we can iterate over the sorted array and execute start commands
```dart
for lg in "${lg_frames_sorted[@]}"; do
  screenNumber=${lg:2}
  if [ "$lg" != "lg1" ]; then
    echo $lg
    sshpass -p $PW ssh -tXn $lg "export DISPLAY=:0; chromium-browser http://lg1:$PORT --start-fullscreen &" &
  fi
  sleep 1
done
```
\
Perfect! Now let’s save the file and create close.sh.\
 \
As open.sh let’s check if the password argument is provided and we will assign the first argument to the password variable.
```dart
if [ -z "$1" ]; then
    echo "Error: No password provided."
    echo "Usage: $0 <password>"
    exit 1
fi
PW="$1"
```
\
Now we can Iterate over the list of frames and execute the stop command.
```dart
. ${HOME}/etc/shell.conf
for lg in $LG_FRAMES; do
  if [ $lg != "lg1" ]; then
    sshpass -p $PW ssh -n $lg "export DISPLAY=:0; pkill chromium-browse; pkill chrome" &
  fi
done
```
\
and finally kill chromium processes on the master.
```dart
export DISPLAY=:0
pkill chromium-browse
pkill chrome
```
\
\________________________________________________________________________________________________________________
## **Usage**
\
Now we have our scripts ready to be used. To run a .sh file we must use bash command from terminal like this:
```terminal
bash open.sh <port> <password>
```
\
or for closing:
```terminal
bash close.sh <password> 
```
\
Where <port> is the port of your service page and <password> is the liquid galaxy sudo password. You can run those commands from SSH or from your Flutter application.\
\
Here is an example of application that implements this logic: [scroll text application](https://github.com/0xbaggi/scroll_text_application)\
\
**That’s all!** \
written by Mattia Baggini

