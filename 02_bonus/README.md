# Bonus - More Dockerfiles

First you need to setup a virtual machine by running commands [01](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/01) & [03](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/03) from [how to docker](https://github.com/dfinnis/Docker/tree/master/00_how_to_docker), also shown below. <br>
```docker-machine create --driver virtualbox Char``` <br>
```eval $(docker-machine env Char)```

Let's add more power to the VM. <br>
```docker-machine stop Char && VBoxManage modifyvm Char --cpus 2 && VBoxManage modifyvm Char --memory 4096 && docker-machine start Char && eval $(docker-machine env Char)```

Now you are ready to launch Dockerfiles. To delete the VM afterwards run: <br>
```docker-machine rm -y Char```


## [0.](https://github.com/dfinnis/Docker/blob/master/02_bonus/b00/Dockerfile) Debian with Python3 dev environment

To build and run: <br>
```docker build -t 00 .``` <br>
```docker run -it --rm 00``` <br>
```python3 max.py``` <br>
```exit```


## [1.](https://github.com/dfinnis/Docker/blob/master/02_bonus/b01/Dockerfile) Debian for basic network testing

To build and run: <br>
```docker build -t b01 .``` <br>
```docker run -it --rm b01``` <br>

Scan the local network: <br>
```nmap {VM_IP}``` <br>
```exit```


## [2.](https://github.com/dfinnis/Docker/blob/master/02_bonus/b02/Dockerfile) Debian with C dev environment

To build and run: <br>
```docker build -t b02 .``` <br>
```docker run -it --rm b02```


## [3.](https://github.com/dfinnis/Docker/blob/master/02_bonus/b03/Dockerfile) Debian with fortune | cowsay

To build and run: <br>
```docker build -t b03 .``` <br>
```docker run -it --rm b03```


## [4.](https://github.com/dfinnis/Docker/blob/master/02_bonus/b04/Dockerfile) Debian with fortune | whalesay

To run: <br>
```docker run docker/whalesay cowsay "Maximum Bonus Points"```
