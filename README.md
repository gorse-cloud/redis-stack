# Redis Cluster

Start a Redis 8 cluster with built-in Search and TimeSeries in GitHub Actions.

## Usage

Use this action in a GitHub Actions workflow to start a Redis cluster before running tests or other CI tasks.

```yaml
- name: Setup Redis cluster
  uses: gorse-cloud/redis-cluster@<tag>
```

The action:

1. starts the six-node Redis 8 cluster via Docker Compose
2. waits until the Redis cluster reports `cluster_state:ok`

After the action finishes, the cluster is available on ports `7000` through `7005`.

## Inputs

| Input | Default | Description |
| --- | --- | --- |
| `port` | `7005` | Redis cluster port used for the health check. |
| `retries` | `12` | Number of health check attempts. |
| `interval-seconds` | `5` | Seconds to wait between health check attempts. |
