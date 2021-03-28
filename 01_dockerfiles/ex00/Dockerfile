## Alpine image with Vim editor
FROM alpine

RUN apk update \
	&& apk upgrade \
	&& apk add vim

CMD ["vim"]

# To build and run:
# docker build -t ex00 .
# docker run -it --rm ex00
