## Debian with Python3 dev environment
FROM debian

RUN apt-get update && apt-get -y upgrade && \
	apt-get install -y python3 python3-pip build-essential libssl-dev libffi-dev python3-dev

	WORKDIR /home/projects

	COPY max.py max.py
	RUN python3 max.py

# To build and run:
# docker build -t 00 .
# docker run -it --rm 00
# python3 max.py
# exit
