FROM openjdk:11-jdk-slim-buster
LABEL maintainer="Hoang Bui <mynamebvh@gmail.com>"

RUN apt update && \
    apt install maven -y

COPY . .
ENTRYPOINT ["sh", "/script.sh"]