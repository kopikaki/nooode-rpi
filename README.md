# nooode-rpi (beta)
Install nooode docker for Raspberry Pi

## Getting Started

### Prerequisites

##### - Raspberry Pi 3B+ / ZERO
##### - OS: Raspbian Stretch with Desktop and Recommended Software

**Follow the link to install Raspbian if you are setting up for a new pi**
```console
https://projects.raspberrypi.org/en/projects/noobs-install
```

### Install Docker

1. Install latest version of Docker
```console
$ curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh
```

2. Create user group, assuming **pi** is login user
```console
$ sudo groupadd docker
$ sudo gpasswd -a pi docker
$ sudo usermod -aG docker pi
```

3. Reboot after installation
```console
$ sudo reboot
```

4. Test Docker installation
```console
$ docker --version
$ docker images
```

### Special Instruction for RPi ZERO

1. You need to downgrade docker version if you install docker to Raspberry Pi ZERO
```console
$ sudo apt-get install docker-ce=18.06.2~ce~3-0~raspbian
```
2. Docker engine will take about 5-10 mins to start after system reboot for RPi ZERO, please be patient.

### Install and Enable I2C Interface

1. Enable I2C from system configuration (Interface Option)

```console
$ sudo raspi-config

Restart Pi after configration.
```

2. Install I2C Python Tools
```console
$ sudo apt-get update
$ sudo apt-get install -y python-smbus i2c-tools
```

3. Wait ten seconds, disconnect the power to your Pi and you are now ready to connect your I2C hardware.


### Install nooode-rpi Docker

1. Download docker image
```console
$ docker pull jeffqu/noderedexp:0.5.3-rpi
```

2. Create working folder (for new installation)
```console
$ mkdir -p $HOME/docker/node-red-exp/data
```

3. Run docker instance with console
```console
$ docker run -it -p 1880:1880 -v $HOME/docker/node-red-exp/data:/usr/src/data -v /lib/modules:/lib/modules --device /dev/i2c-0 --device /dev/i2c-1 --privileged --user 0 --restart unless-stopped --name noderedexp jeffqu/noderedexp:0.5.1-rpi

//Press Ctrl P and Ctrl Q to exist from console.
```

4. Docker instance is auto-started everytime when system reboots.


### Upgrade nooode-rpi Docker

1. Stop and remove docker
```console
$ docker stop noderedexp
$ docker rm noderedexp
```
2. Follow the previous steps to download and run new docker image


### Running

Open the link in web browser
```console
http://{ip address of Pi}:1880
```

## Version
* v0.5.3

## Authors
* Jeffrey Qu

## License
* MIT Licens
