FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install -y git cmake
RUN git clone https://github.com/srsLTE/srsLTE.git
WORKDIR srsLTE
RUN git checkout release_19_12
RUN mkdir build
RUN apt-get install -y g++
RUN apt-get install -y libmbedtls-dev
RUN apt-get install -y libconfig++-dev
RUN apt-get install -y libsctp-dev
RUN apt-get install -y libboost-all-dev
RUN apt-get install -y libfftw3-dev
RUN DEBIAN_FRONTEND=noninteractive apt install -y tzdata
RUN apt-get install -y uhd-host libuhd003.010.003 libuhd-dev
RUN cd build && cmake ../
RUN cd build && make
#RUN cd build && make test
RUN cd build && make install
RUN cd build && srslte_install_configs.sh user
RUN ldconfig
RUN uhd_images_downloader

COPY epc.conf /root/.config/srslte/epc.conf
COPY enb.conf /root/.config/srslte/enb.conf
COPY user_db.csv /root/.config/srslte/user_db.csv

CMD srsenb
