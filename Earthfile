VERSION 0.8
FROM ubuntu:22.04

RUN apt-get update && apt-get install -y git

all:
    BUILD +redisearch
    BUILD +redistimeseries

redisearch:
    WORKDIR /RediSearch
    RUN git clone --recursive --depth 1 --branch v2.10.10 https://github.com/RediSearch/RediSearch.git /RediSearch
    RUN cd .install && ./install_script.sh && ./install_boost.sh 1.83.0
    RUN make setup && make build COORD=1
    SAVE ARTIFACT /RediSearch/bin/linux-x64-release/coord-oss/module-oss.so AS LOCAL modules/module-oss.so

redistimeseries:
    WORKDIR /RedisTimeSeries
    RUN git clone --recursive --depth 1 --branch v1.12.5 https://github.com/RedisTimeSeries/RedisTimeSeries.git /RedisTimeSeries
    RUN ./sbin/setup && bash -l && make
    SAVE ARTIFACT /RedisTimeSeries/bin/linux-x64-release/redistimeseries.so AS LOCAL modules/redistimeseries.so
