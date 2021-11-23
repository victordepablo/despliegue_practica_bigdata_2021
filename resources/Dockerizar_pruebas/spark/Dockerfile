FROM ubuntu:20.04

ENV TZ=Europe
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# GIT
RUN apt-get update -y
RUN apt install git-all -y

# JAVA
RUN apt install openjdk-8-jre -y
ENV JAVA_HOME /usr/lib/jvm/java-1.8.0-openjdk-amd64
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
ENV SPARK_HOME /spark-3.1.2-bin-hadoop3.2
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
  
# Descarga de datos de vuelo
WORKDIR /
RUN git clone https://github.com/ging/practica_big_data_2019
WORKDIR /practica_big_data_2019
RUN resources/download_data.sh

# Instalar python3.7
RUN apt install software-properties-common -y
RUN add-apt-repository ppa:deadsnakes/ppa
RUN apt-get update -y
RUN apt-get install python3.7 -y
RUN apt-get install python3-pip -y
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 1

# Instalar libreria de python con Dockerfile web
WORKDIR /practica_big_data_2019
RUN pip install -r /practica_big_data_2019/requirements.txt
RUN pip3 install Pillow
ENV PROJECT_HOME=/practica_big_data_2019/
RUN python3.7

# Entrenar el modelo no es necesario ya que al bajarnos nuestro proyecto clonado ya esta entrenado
RUN python3.7 resources/train_spark_mllib_model.py .

# Run Flight Predictor
WORKDIR /practica_big_data_2019/flight_prediction/src/main/scala/es/upm/dit/ging/predictor/
CMD ["sbt compile"]
CMD ["sbt package"]

# SPARK-SUBMIT
EXPOSE 7077 8080 6066
WORKDIR /spark-3.1.2-bin-hadoop3.2/bin/
COPY spark-submit /spark-3.1.2-bin-hadoop3.2/bin
CMD ["spark-submit --class es.upm.dit.ging.predictor.MakePrediction --packages org.mongodb.spark:mongo-spark-connector_2.12:3.0.1,org.apache.spark:spark-sql-kafka-0-10_2.12:3.1.2 /home/victor/Escritorio/practica_prediccion_vuelos/practica_big_data_2019/flight_prediction/target/scala-2.12/flight_prediction_2.12-0.1.jar"]
  




  






