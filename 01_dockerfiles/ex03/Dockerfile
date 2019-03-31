FROM debian

# 443/80: HTTPS/internet
# 22: SSH
EXPOSE 443 80 22

RUN apt-get update && DEBIAN_FRONTEND=noninteractive \
	apt-get upgrade -y && \
	apt-get install -y ca-certificates openssh-server wget postfix

RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh && \
	chmod +x script.deb.sh && ./script.deb.sh && \
	apt-get install -y gitlab-ce

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /etc/gitlab/ssl
RUN chmod 700 /etc/gitlab/ssl
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
	-subj /C=FR/ST=0/L=Paris/O=42/OU=0/CN=192.168.99.102/emailAddress=aschukin@student.42.fr \
	-keyout /etc/gitlab/ssl/selfsigned.key -out /etc/gitlab/ssl/selfsigned.crt

RUN echo "external_url \"https://192.168.99.100\"" >> /etc/gitlab/gitlab.rb
RUN echo "nginx['redirect_http_to_https'] = true" >> /etc/gitlab/gitlab.rb
RUN echo "nginx['ssl_certificate'] = \"/etc/gitlab/ssl/selfsigned.crt\"" >> /etc/gitlab/gitlab.rb
RUN echo "nginx['ssl_certificate_key'] = \"/etc/gitlab/ssl/selfsigned.key\"" >> /etc/gitlab/gitlab.rb
RUN echo "gitlab_rails['gitlab_shell_ssh_port'] = 2200" >> /etc/gitlab/gitlab.rb

ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) && \
			gitlab-ctl reconfigure && service ssh start && gitlab-ctl tail

# docker build -t ex03 .
# docker run -it --rm -p 80:80 -p 2200:22 -p 443:443 --privileged ex03

# add more power to the VM:
# docker-machine stop Char && VBoxManage modifyvm Char --cpus 2 && VBoxManage modifyvm Char --memory 4096 && docker-machine start Char && eval $(docker-machine env Char)

# access web client, create a user and interact via GIT:
# Type the external_url into your web browser: 'https://192.168.99.100'
# Create your new Gitlab password
# Log in with 'root' as your username + your new password
# create a new git repo
# export GIT_SSL_NO_VERIFY=true git clone <https://repo_address.git>