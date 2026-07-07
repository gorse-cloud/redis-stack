# Redis Cluster

Start a Redis cluster with RediSearch and RedisTimeSeries modules loaded in GitHub Actions.

## Usage

Use this action in a GitHub Actions workflow to start a Redis cluster before running tests or other CI tasks.

```yaml
- name: Setup Redis cluster
  uses: gorse-cloud/redis-cluster@<tag>
```

The action:

1. downloads `module-oss.so` and `redistimeseries.so` from a `gorse-cloud/redis-cluster` GitHub release
2. starts the six-node Redis cluster via Docker Compose
3. waits until Redis replies to `PING`

After the action finishes, the cluster is available on ports `7000` through `7005`.

## Inputs

| Input | Default | Description |
| --- | --- | --- |
| `release-tag` | `""` | GitHub release tag to download module artifacts from. Empty uses the latest release. |
| `port` | `7005` | Redis cluster port used for the health check. |
| `retries` | `12` | Number of health check attempts. |
| `interval-seconds` | `5` | Seconds to wait between health check attempts. |
