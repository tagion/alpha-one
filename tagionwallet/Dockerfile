FROM ubuntu:20.04

RUN apt-get update && apt-get upgrade -y && apt-get install libssl1.1 -y && apt install curl -y

WORKDIR /usr/local/bin/
COPY ./tagionwallet .

WORKDIR /files/