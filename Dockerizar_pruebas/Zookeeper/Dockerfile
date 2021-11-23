FROM centos:7
RUN yum -y update
RUN yum -y install vim
RUN yum -y install nc 
RUN yum -y install lsof
RUN yum -y install java-11-openjdk-devel
RUN echo 'JAVA_HOME="/usr/lib/jvm/java-11-openjdk-11.0.6.10-1.e17_7.x86_64/bin/java"' >> ~/.bashrc
RUN source ~/.bashrc
COPY Zookeeper1 /opt/Zookeeper1
WORKDIR /opt/Zookeeper1
