# Raspberry Pi Kubernetes Cluster

## Todo 
- ~~install Ubuntu Server~~
- ~~wifi configs~~ 
- ~~ssh in~~
- ~~setup docker~~
- install minkube
- create postgres cluster
- connect to it remotely with pgadmin or something of the sorts

## What you need

- a Raspberry PI. we're using a *Raspberry Pi 4 Model B 8GB*
- a memory card for the Pi's OS. either SD or microSD, depending on your Pi
- a LAN network with internet access
- a computer that can run the Raspberry Pi Imager (see below) and connect to the Pi via SSH

Some of the commands below are `macOS` specific.

## Install Ubuntu Server OS

- download and install the [Raspberry Pi Imager](https://www.raspberrypi.org/downloads/)
- mount the SD card that will hold your Pi's OS
- start the installer and follow the instructions to install `Ubuntu Server 20.x`

Once the installer has finished, navigate to the root directory of the
mounted SD card volume and create an empty `ssh` file. This will
allow you to connect to the Pi using SSH later:

    touch ssh

Open `which file was that again?` and find the following lines. Uncomment them,
then replace `SSID-NAME-HERE` and `PASSWORD-HERE` with your wifi network's
name and password. Make sure to surround both the name and password with
quotes `"..."`.

    wifis:
    wlan0:
        optional: true
        access-points:
            "SSID-NAME-HERE":
                password: "PASSWORD-HERE"
        dhcp4: true

Save all changes, then unmount the SD card, insert it into your Pi and start
it!

## Connect via SSH

After a couple of seconds, your Pi should have booted and connected to the
wifi network. Connect to the same network as your Pi, then find its IP address
in the list of connected devices:

    # brew install nmap
    nmap -sn 192.168.1.0/24

Then access your Pi via `ssh`. The user and password are `ubuntu`:

    ssh ubuntu@<IP ADDRESS>

Follow the password reset dialog, then exit and reconnect. Done!

## Disable Swap

To prolong the lifetime of your SD card, disable memory swap (to avoid
excessive writes to the drive).

    sudo sed -i '/ swap / s/^/#/' /etc/fstab

## Assign Static IP Address

## Add SSH Key (Optional)

## Install Docker

Follow [these instructions](https://phoenixnap.com/kb/install-docker-on-ubuntu-20-04)
to install Docker on Ubuntu. If `apt` fails to find suitable install
candidates, try:
 
    sudo apt-get install -y docker.io

To avoid having to run Docker with `sudo`:

    sudo usermod -aG docker ubuntu
    sudo reboot

To check that everything works as expected:

    docker run hello-world

## Install Minikube

    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin/minikube

## Useful Links
- [image loader for raspberry pi](https://www.raspberrypi.org/downloads/)
- [headless raspberry pi tutorial](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md)
- [connect to headless pi](https://www.raspberrypi.org/documentation/remote-access/ip-address.md)
- [high level ubuntu headless](https://atelierhsn.com/2020/06/raspi-headless-setup/)
- [Docker on Ubuntu](https://phoenixnap.com/kb/install-docker-on-ubuntu-20-04)