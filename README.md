# RediSearch

Load RediSearch module into Redis cluster.

## Build and release modules

Redis module `.so` artifacts are built by GitHub Actions when a GitHub release is published. The release workflow clones RediSearch and RedisTimeSeries, runs their build commands directly, and uploads the generated files to the same GitHub release:

- `module-oss.so`
- `redistimeseries.so`

To publish new artifacts, create and publish a GitHub release for the desired tag.

## Download released modules

Download the `.so` files from a GitHub release before starting the Redis cluster:

```bash
mkdir -p modules
gh release download <tag> --repo gorse-cloud/redis-cluster --pattern '*.so' --dir modules
```

## Build modules locally

Build RediSearch with coordinator support:

```bash
repo=$(pwd)
git clone --recursive --depth 1 --branch v2.10.10 https://github.com/RediSearch/RediSearch.git /tmp/RediSearch
cd /tmp/RediSearch
cd .install
./install_script.sh sudo
./install_boost.sh 1.83.0
cd ..
make setup
make build COORD=1
mkdir -p "$repo/modules"
cp /tmp/RediSearch/bin/linux-x64-release/coord-oss/module-oss.so "$repo/modules/module-oss.so"
```

Build RedisTimeSeries:

```bash
repo=$(pwd)
git clone --recursive --depth 1 --branch v1.12.5 https://github.com/RedisTimeSeries/RedisTimeSeries.git /tmp/RedisTimeSeries
cd /tmp/RedisTimeSeries
./sbin/setup
bash -lc 'make'
mkdir -p "$repo/modules"
cp /tmp/RedisTimeSeries/bin/linux-x64-release/redistimeseries.so "$repo/modules/redistimeseries.so"
```

## Run Redis cluster

```bash
docker compose up -d
```

Connect to Redis cluster:

```bash
redis-cli -c -h localhost -p 7005
```
