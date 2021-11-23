FROM mongo:4.2
RUN apt-get update -y
RUN apt install git-all -y
WORKDIR /
RUN git clone https://github.com/ging/practica_big_data_2019
WORKDIR /practica_big_data_2019
EXPOSE 27017
CMD ["resources/import_distances.sh"]

