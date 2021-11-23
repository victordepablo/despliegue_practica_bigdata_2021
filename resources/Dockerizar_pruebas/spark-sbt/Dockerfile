FROM ubuntu:20.04

ENV TZ=Europe
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# GIT
RUN apt-get update -y
RUN apt install git-all -y

# JAVA
RUN apt install openjdk-8-jre -y

# SCALA
RUN apt install scala -y

# wget
RUN apt install wget -y

# curl
RUN apt install curl -y

# SPARK

WORKDIR /

# spark-3.1.2-bin-hadoop2.7
RUN wget https://dlcdn.apache.org/spark/spark-3.1.2/spark-3.1.2-bin-hadoop3.2.tgz && tar -zxvf spark-3.1.2-bin-hadoop3.2.tgz && rm spark-3.1.2-bin-hadoop3.2.tgz
WORKDIR /spark-3.1.2-bin-hadoop3.2/sbin/
COPY start-master.sh /spark-3.1.2-bin-hadoop3.2/sbin/
CMD ["./start-master.sh"]

# SBT

WORKDIR /

ARG SBT_VERSION=1.5.5
RUN \
  mkdir /working/ && \
  cd /working/ && \
  curl -L -o sbt-$SBT_VERSION.deb https://repo.scala-sbt.org/scalasbt/debian/sbt-$SBT_VERSION.deb && \
  dpkg -i sbt-$SBT_VERSION.deb && \
  rm sbt-$SBT_VERSION.deb && \
  apt-get update && \
  apt-get install sbt && \
  cd && \
  rm -r /working/ && \
  sbt sbtVersion
  






