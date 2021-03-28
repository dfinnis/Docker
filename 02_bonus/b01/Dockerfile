## Debian for basic network testing
FROM debian

RUN apt-get update && apt-get upgrade -y && \
	apt-get install -y vim net-tools nmap

# To build and run:
# docker build -t b01 .
# docker run -it --rm b01

# Scan the local network:
# nmap {VM_IP}
# exit
