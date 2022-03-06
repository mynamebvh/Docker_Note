FROM openjdk:11
LABEL maintainer="Hoang Bui <mynamebvh@gmail.com>"

RUN apt update && \
    apt install maven -y

COPY . .
CMD mvn clean package
