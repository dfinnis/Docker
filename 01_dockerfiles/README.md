# Dockerfiles

First you need to setup a virtual machine by running commands [01](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/01) & [03](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/03) from [how to docker](https://github.com/dfinnis/Docker/tree/master/00_how_to_docker), also shown below. <br>
```docker-machine create --driver virtualbox Char``` <br>
```eval $(docker-machine env Char)```

Now you are ready to launch Dockerfiles. To delete the VM afterwards run: <br>
```docker-machine rm -y Char```

## [0.](https://github.com/dfinnis/Docker/blob/master/01_dockerfiles/ex00/Dockerfile) Alpine image with Vim editor

To build and run: <br>
```docker build -t ex00 .``` <br>
```docker run -it --rm ex00```

## [1.](https://github.com/dfinnis/Docker/blob/master/01_dockerfiles/ex01/Dockerfile) Debian TeamSpeak server

To build and run: <br>
```docker build -t ex01 .``` <br>
```docker run -it -p 9987:9987/udp -p 10011:10011 -p 30033 --rm ex01```

* launch Teamspeak
* Continue without logging in
* Choose your nickname: Drew
* Drop down menu: Connections -> Connect
* Replace "server nickname or address" with the IP address of the container ([how_to_docker/02](https://github.com/dfinnis/Docker/blob/master/00_how_to_docker/01))
* Copy in ServerAdmin privilege key that appears in terminal
* Enter Chat Message

Port notes:
* 9987 = default voice
* 10011 = server query
* 30033 = file transport

## [2.](https://github.com/dfinnis/Docker/blob/master/01_dockerfiles/ex02/Dockerfile) Ruby container for Rails applications

1. Build. <br>
```docker build -t ft-rails:on-build .```

2. git clone a ruby test app from [here](https://bitbucket.org/railstutorial/sample_app_4th_ed.git) or [here](https://github.com/RailsApps/rails-signup-thankyou).

3. modify the sample_app's Gemfile.lock: <br>
rake (12.3.1) -> rake (12.3.2)

4. Go into git repo for ruby app and create a Dockerfile, copy-paste the following: <br>
```
FROM ft-rails:on-build

EXPOSE 3000
CMD ["rails", "s", "-b", “0.0.0.0”, “-p”, "3000"]
```

5. Build and run. <br>
```cd ..``` (out of sample_app, and back to ex02) <br>
```docker build -t ex02 .``` <br>
```docker run -it --rm -p 3000:3000 ex02``` <br>

6. Example ruby instructions: <br>
```print "Hello Ruby!\n"``` <br>
```40 + 2```

## [3.](https://github.com/dfinnis/Docker/blob/master/01_dockerfiles/ex03/Dockerfile) Debian with Gitlab server (SSL and SSH)

1. Build and run: <br>
```docker build -t ex03 .``` <br>
```docker run -it --rm -p 80:80 -p 2200:22 -p 443:443 --privileged ex03```

2. Add more power to the VM: <br>
```docker-machine stop Char && VBoxManage modifyvm Char --cpus 2 && VBoxManage modifyvm Char --memory 4096 && docker-machine start Char && eval $(docker-machine env Char)```

3. Access web client, create a user and interact via GIT: <br>
    * Type the external_url into your web browser.
    * Create your new Gitlab password.
    * Log in with 'root' as your username + your new password
    * create a new git repo. <br>
```GIT_SSL_NO_VERIFY=true git clone <https://repo_address.git>```

Port notes:
* 443/80: HTTPS/internet
* 22: SSH
