FROM ubuntu:20.04
RUN apt-get update -y
RUN apt install software-properties-common -y
RUN add-apt-repository ppa:deadsnakes/ppa
RUN apt-get update -y
RUN apt-get install python3.7 -y
RUN apt-get install python3-pip -y
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 1
WORKDIR /
RUN apt install git-all -y
RUN git clone https://github.com/ging/practica_big_data_2019
RUN cd practica_big_data_2019/
RUN pip install -r /practica_big_data_2019/requirements.txt
RUN pip3 install Pillow
ENV PROJECT_HOME=/practica_big_data_2019/
EXPOSE 9500 9600
CMD ["python3.7", "/practica_big_data_2019/resources/web/predict_flask.py"]

