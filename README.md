# Pi for all

## Todo 
- ~~install raspian~~
- ~~wifi configs~~ 
- ~~ssh in~~ 
- ~~setup docker~~
- create postgres kube cluster thingie
- connect to it remotely with pgadmin or something of the sorts

## Connect via SSH

Get IP adddress

    ifconfig | grep inet

Scan network and find the IP address of your Pi:

    # brew install nmap
    nmap -sn 192.168.1.0/24

Then connect using `ssh`:

    # initial pass ubuntu
    ssh ubuntu@192.168.1.235

Follow the password reset dialog, then reconnect. Done!

## Install Docker

If no Docker candidates are found:
 
    sudo apt-get install -y docker.io

To avoid having to run Docker with `sudo` all the time:

    sudo usermod -aG docker ubuntu
    sudo reboot

To check that everything works as expected:

    docker run hello-world

## Links
- [image loader for raspberry pi](https://www.raspberrypi.org/downloads/)
- [headless raspberry pi tutorial](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md)
- [connect to headless pi](https://www.raspberrypi.org/documentation/remote-access/ip-address.md)
- [high level ubuntu headless](https://atelierhsn.com/2020/06/raspi-headless-setup/)
- [Docker on Ubuntu](https://phoenixnap.com/kb/install-docker-on-ubuntu-20-04)