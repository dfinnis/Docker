## Debian with fortune | cowsay
FROM debian

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y cowsay fortune

ENTRYPOINT /usr/games/fortune | /usr/games/cowsay -f ghostbusters

# To build and run:
# docker build -t b03 .
# docker run -it --rm b03
