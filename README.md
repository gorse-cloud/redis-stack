# RediSearch

Load RediSearch module into Redis cluster.

1. Install Earthly.

```bash
sudo /bin/sh -c 'wget https://github.com/earthly/earthly/releases/latest/download/earthly-linux-amd64 -O /usr/local/bin/earthly && chmod +x /usr/local/bin/earthly && /usr/local/bin/earthly bootstrap --with-autocomplete'
```

2. Build RediSearch and RedisTimeSeries module with coordinator.

```bash
earthly +all
```

3. Setup Redis cluster.

```bash
docker compose up -d
```

4. Connect to Redis cluster.

```bash
redis-cli -c -h localhost -p 7005
```
