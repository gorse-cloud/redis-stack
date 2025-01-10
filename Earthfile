VERSION 0.7
FROM ubuntu:22.04

WORKDIR /RediSearch

build:
    RUN apt-get update && apt-get install -y git
    RUN git clone --recursive --depth 1 --branch v2.10.10 https://github.com/RediSearch/RediSearch.git /RediSearch
    RUN cd .install && ./install_script.sh && ./install_boost.sh 1.83.0
    RUN make setup && make build COORD=1
    SAVE ARTIFACT /RediSearch/bin/linux-x64-release/coord-oss/module-oss.so AS LOCAL modules/module-oss.so
