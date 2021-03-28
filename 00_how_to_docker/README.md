# How to Docker

All the files can be run directly. For example:<br>
```./01```
<br>


## Setup

**[1.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/01) Create a virtual machine with docker-machine using the virtualbox driver, and named Char.**

```
docker-machine create --driver virtualbox Char
```
To test run: ```docker-machine ls```
<br>
<br>


**[2.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/02) Get the IP address of the Char virtual machine.**

```
docker-machine ip Char
```
<br>


**[3.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/03) Define the variables needed by your virtual machine Char in the general env of your terminal, so that you can run the docker ps command without errors. You have to fix all four environment variables with one command, and you are not allowed to use your shell’s builtin to set these variables by hand.**

```
eval $(docker-machine env Char)
```
To test run: ```docker ps```
<br>
<br>


## Containers

**[4.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/04) Get the hello-world container from the Docker Hub, where it’s available.**

```
docker pull hello-world
```
To test run: ```docker image ls```
<br>
<br>


**[5.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/05) Launch the hello-world container, and make sure that it prints its welcome message, then leaves it.**

```
docker run hello-world
```
<br>


**[6.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/06) Launch an nginx container, available on Docker Hub, as a background task. It should be named overlord, be able to restart on its own, and have its 80 port attached to the 5000 port of Char. You can check that your container functions properly by visiting http://<ip-de-char>:5000 in your web browser.**

```
docker run -d -p 5000:80 --name overlord --restart=always nginx
```
To test navigate to the following address in a web browser: {VM_IP}:5000/
<br>
<br>


**[7.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/07) Get the internal IP address of the overlord container without starting its shell and in one command.**

```
docker inspect -f '{{.NetworkSettings.IPAddress}}' overlord
```
<br>


**[8.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/08) Launch a shell from an alpine container, and make sure that you can interact directly with the container via your terminal, and that the container deletes itself once the shell’s execution is done.**

```
docker run -it --rm alpine /bin/sh
```
<br>


**[9.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/09) From the shell of a debian container, install via the container’s package manager everything you need to compile C source code and push it onto a git repo (of course, make sure before that the package manager and the packages already in the container are updated). For this exercise, you should only specify the commands to be run directly in the container.**

```
apt-get update && apt-get upgrade -y && apt-get install -y gcc make git
```
To launch an debian container: ```docker run -it --rm debian```
<br>
<br>


## Volumes

**[10.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/10) Create a volume named *hatchery*.**

```
docker volume create --name hatchery
```
<br>


**[11.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/11) List all the Docker volumes created on the machine.**

```
docker volume ls
```
<br>


**[12.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/12) Launch a mysql container as a background task. It should be able to restart on its own in case of error, and the root password of the database should be Kerrigan. You will also make sure that the database is stored in the hatchery volume, that the container directly creates a database named zerglings, and that the container itself is named spawning-pool.**

```
docker run -d --name spawning-pool --restart always -e MYSQL_ROOT_PASSWORD=Kerrigan -e MYSQL_DATABASE=zerglings -v hatchery:/var/lib/mysql mysql:5.7
```
<br>


**[13.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/13) Print the environment variables of the spawning-pool container in one command, to be sure that you have configured your container properly.**

```
docker inspect -f '{{range $index, $value := .Config.Env}}{{println $value}}{{end}}' spawning-pool
```
<br>


**[14.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/14) Launch a wordpress container as a background task, just for fun. The container should be named lair, its 80 port should be bound to the 8080 port of the virtual machine, and it should be able to use the spawning-pool container as a database service. You can try to access lair on your machine via a web browser, with the IP address of the virtual machine as a URL.
Congratulations, you just deployed a functional Wordpress website in two commands!**

```
docker run -d --name lair -p 8080:80 --link spawning-pool:mysql wordpress
```
To test, navigate to the following address in a web browser: {VM_IP}:8080
<br>
<br>


**[15.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/15) Launch a phpmyadmin container as a background task. It should be named roach-warden, its 80 port should be bound to the 8081 port of the virtual machine and it should be able to explore the database stored in the spawning-pool container.**

```
docker run --name roach-warden  -d --link spawning-pool:db -p 8081:80 phpmyadmin/phpmyadmin
```
To test, navigate to the following address in a web browser: {VM_IP}:8081
<br>
<br>


**[16.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/16) Look up the spawning-pool container’s logs in real time without running its shell.**

```
docker logs -f spawning-pool
```
<br>


**[17.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/17) Display all the currently active containers on the Char virtual machine.**

```
docker ps
```
<br>


**[18.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/18) Relaunch the overlord container.**

```
docker restart overlord
```
<br>


**[19.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/19) You will personalize this container so that you can use the Flask micro-framework in its latest version. You will make sure that an html page displaying "Hello World" with \<h1> tags can be served by Flask. You will test that your container is properly set up by accessing, via curl or a web browser, the IP address of your virtual machine on the 3000 port.
You will also list all the necessary commands in your repository.**

```
docker run --name Abathur -v ~/:/root -p 3000:3000 -itd python:2-slim
docker exec Abathur pip install Flask
echo 'from flask import Flask\napp = Flask(__name__)\n@app.route("/")\ndef hello_world():\n\treturn "<h1>Hello, World!</h1>"' > ~/app.py
docker exec --env FLASK_APP=/root/app.py Abathur flask run --host=0.0.0.0 --port 3000
```
To test, navigate to the following address in a web browser: {VM_IP}:3000
<br>
<br>


## Swarm

**[20.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/20) Create a local swarm, the Char virtual machine should be its manager.**

```
docker swarm init --advertise-addr $(docker-machine ip Char)
```
To test run:
```docker info```
```docker node ls```
<br>
<br>


**[21.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/21) Create another virtual machine with docker-machine using the virtualbox driver, and name it Aiur.**

```
docker-machine create --driver virtualbox Aiur
```
<br>


**[22.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/22) Turn Aiur into a slave of the local swarm in which Char is leader (the command to take control of Aiur is not requested).**

```
docker-machine ssh Aiur "docker swarm join --token $(docker swarm join-token -q worker) $(docker-machine ip Char):2377"
```
To test run: ```docker node ls```
<br>
<br>


**[23.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/23) Create an overlay-type internal network that you will name overmind.**

```
docker network create -d overlay overmind
```
To test run: ```docker network ls```
<br>
<br>


**[24.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/24) Launch a rabbitmq SERVICE that will be named orbital-command. You should define a specific user and password for the RabbitMQ service, they can be whatever you want. This service will be on the overmind network.**

```
docker-machine ssh Char "docker service create --name orbital-command --network overmind -e RABBITMQ_DEFAULT_USER=docker -e RABBITMQ_DEFAULT_PASS=docker -d rabbitmq"
```
<br>


**[25.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/25) List all the services of the local swarm.**

```
docker service ls
```
<br>


**[26.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/26) Launch a 42school/engineering-bay service in two replicas and make sure that the service works properly (see the documentation provided at hub.docker.com). This service will be named engineering-bay and will be on the overmind network.**

```
docker-machine ssh Char "docker service create --name engineering-bay --replicas 2 --network overmind -e OC_USERNAME=docker -e OC_PASSWD=docker -d 42school/engineering-bay"
```
To test run: ```docker service ps engineering-bay```
<br>
<br>


**[27.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/27) Get the real-time logs of one the tasks of the engineering-bay service.**

```
docker service logs -f engineering-bay
```
<br>


**[28.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/28) ... Damn it, a group of zergs is attacking orbital-command, and shutting down the engineering-bay service won’t help at all... You must send a troup of Marines to eliminate the intruders. Launch a 42school/marine-squad in two replicas, and make sure that the service works properly (see the documentation provided at hub.docker.com). This service will be named... marines and will be on the overmind network.**

```
docker service create -d --network overmind --name marines --replicas 2 -e OC_USERNAME=root -e OC_PASSWD=root 42school/marine-squad
```
<br>


**[29.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/29) Display all the tasks of the marines service.**

```
docker service ps marines
```
<br>


**[30.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/30) Increase the number of copies of the marines service up to twenty, because there’s never enough Marines to eliminate Zergs. (Remember to take a look at the tasks and logs of the service, you’ll see, it’s fun.)**

```
docker service scale -d marines=20
```
To test run:
```docker service ps marines```
```docker service logs -f $(docker service ps marines -f "name=marines.11" -q)```
<br>
<br>


## Cleanup

**[31.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/31) Force quit and delete all the services on the local swarm, in one command.**

```
docker service rm $(docker service ls -q)
```
To test run: ```docker service ls```
<br>
<br>


**[32.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/32) Force quit and delete all the containers (whatever their status), in one command.**

```
docker rm -f $(docker ps -a -q)
```
To test run: ```docker images ls```
<br>
<br>


**[33.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/33) Delete all the container images stored on the Char virtual machine, in one command as well.**

```
docker rmi $(docker images -a -q)
```
To test run: ```docker-machine ls```
<br>
<br>


**[34.](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/34) Delete the Aiur virtual machine without using rm -rf.**

```
docker-machine rm -y Aiur
```
To test run: ```docker-machine ls```
