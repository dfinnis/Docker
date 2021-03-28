# How to Docker



1. Create a virtual machine with docker-machine using the virtualbox driver, and named Char.
2. Get the IP address of the Char virtual machine.
3. Define the variables needed by your virtual machine Char in the general env of your terminal, so that you can run the docker ps command without errors. You have to fix all four environment variables with one command, and you are not allowed to use your shell’s builtin to set these variables by hand.
4. Get the hello-world container from the Docker Hub, where it’s available.
5. Launch the hello-world container, and make sure that it prints its welcome mes-
sage, then leaves it.
6. Launch an nginx container, available on Docker Hub, as a background task. It should be named overlord, be able to restart on its own, and have its 80 port attached to the 5000 port of Char. You can check that your container functions properly by visiting
http://<ip-de-char>:5000 on your web browser.
7. Get the internal IP address of the overlord container without starting its shell and
in one command.
8. Launch a shell from an alpine container, and make sure that you can interact directly with the container via your terminal, and that the container deletes itself once the shell’s execution is done.
9. From the shell of a debian container, install via the container’s package manager everything you need to compile C source code and push it onto a git repo (of course, make sure before that the package manager and the packages already in the container are updated). For this exercise, you should only specify the commands to be run directly in the container.
10. Create a volume named hatchery.
11. List all the Docker volumes created on the machine. Remember. VOLUMES.
12. Launch a mysql container as a background task. It should be able to restart on its own in case of error, and the root password of the database should be Kerrigan. You will also make sure that the database is stored in the hatchery volume, that the container directly creates a database named zerglings, and that the container itself is named spawning-pool.
13. Print the environment variables of the spawning-pool container in one command, to be sure that you have configured your container properly.
14. Launch a wordpress container as a background task, just for fun. The container should be named lair, its 80 port should be bound to the 8080 port of the virtual machine, and it should be able to use the spawning-pool container as a database service. You can try to access lair on your machine via a web browser, with the IP address of the virtual machine as a URL.
Congratulations, you just deployed a functional Wordpress website in two com- mands!
15. Launch a phpmyadmin container as a background task. It should be named roach-warden, its 80 port should be bound to the 8081 port of the virtual machine and it should
be able to explore the database stored in the spawning-pool container.
16. Look up the spawning-pool container’s logs in real time without running its shell.
17. Display all the currently active containers on the Char virtual machine.
18. Relaunch the overlord container.
19. Launch a container name Abathur. It will be a Python container, 2-slim version, its /root folder will be bound to a HOME folder on your host, and its 3000 port will be bound to the 3000 port of your virtual machine.
You will personalize this container so that you can use the Flask micro-framework in its latest version. You will make sure that an html page displaying "Hello World" with \<h1> tags can be served by Flask. You will test that your container is properly set up by accessing, via curl or a web browser, the IP address of your virtual machine on the 3000 port.
You will also list all the necessary commands in your repository.
20. Create a local swarm, the Char virtual machine should be its manager.
21. Create another virtual machine with docker-machine using the virtualbox driver, and name it Aiur.
22. Turn Aiur into a slave of the local swarm in which Char is leader (the command to take control of Aiur is not requested).
23. Create an overlay-type internal network that you will name overmind.
24. Launch a rabbitmq SERVICE that will be named orbital-command. You should define a specific user and password for the RabbitMQ service, they can be whatever you want. This service will be on the overmind network.
25. List all the services of the local swarm.
26. Launch a 42school/engineering-bay service in two replicas and make sure that the service works properly (see the documentation provided at hub.docker.com). This service will be named engineering-bay and will be on the overmind network.
27. Get the real-time logs of one the tasks of the engineering-bay service.
28. ... Damn it, a group of zergs is attacking orbital-command, and shutting down the engineering-bay service won’t help at all... You must send a troup of Marines to eliminate the intruders. Launch a 42school/marine-squad in two replicas, and make sure that the service works properly (see the documentation provided at hub.docker.com). This service will be named... marines and will be on the overmind network.
29. Display all the tasks of the marines service.
30. Increase the number of copies of the marines service up to twenty, because there’s never enough Marines to eliminate Zergs. (Remember to take a look at the tasks and logs of the service, you’ll see, it’s fun.)
31. Force quit and delete all the services on the local swarm, in one command.
32. Force quit and delete all the containers (whatever their status), in one command.
33. Delete all the container images stored on the Char virtual machine, in one command as well.
34. Delete the Aiur virtual machine without using rm -rf.
