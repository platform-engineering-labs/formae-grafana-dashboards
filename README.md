# Formae Grafana Dashboards

Pre-built Grafana dashboards for monitoring [formae](https://github.com/platform-engineering-labs/formae) infrastructure.

## Dashboards

### Formae Agent

A comprehensive dashboard for monitoring the formae agent:

| Section | Metrics |
|---------|---------|
| **Formae Stats** | Stacks, targets, managed/unmanaged resources, clients, agent uptime, resource errors, commands by state/type |
| **Host Metrics** | CPU, memory, network I/O, disk throughput and IOPS |
| **Process** | Agent CPU and memory usage |
| **Go Runtime** | Goroutines, memory in use, GC pressure, allocation rate |
| **Ergo Node Metrics** | Node uptime, applications, processes, zombie processes, memory, CPU, registered entities |
| **Ergo Network Metrics** | Connected nodes, remote messages and bytes, connection uptime |
| **Database** | Connection pool, query rate and duration, pool health, slowest queries |
| **Rate Limiter** | Token request rate, bucket utilization, available tokens, grant efficiency |
| **Plugin Metrics** | Operation duration, rate, success rate, retries |
| **Logs** | Application logs with level filtering |

### Formae Plugins

A dedicated dashboard for monitoring formae plugins:

| Section | Metrics |
|---------|---------|
| **Plugin Stats** | Targets, managed/unmanaged resources, node uptime, connected nodes, goroutines, resource errors |
| **Process** | Plugin CPU and memory usage |
| **Go Runtime** | Goroutines, memory in use, allocation rate, GC pressure |
| **Ergo Node Metrics** | Processes, zombie processes, memory, CPU, registered entities |
| **Ergo Network Metrics** | Remote messages and bytes, connection uptime |
| **Plugin Metrics** | Operation duration, rate, success rate, retries |
| **Logs** | Plugin logs filtered by plugin name prefix |

## Installation

### Manual Import

1. Download the dashboard JSON files from the `dashboards/` directory:
   - `formae-overview.json` (Formae Agent)
   - `formae-plugin.json` (Formae Plugins)
2. In Grafana, navigate to **Dashboards > Import**
3. Upload the JSON file or paste its contents
4. Select your Prometheus and Loki datasources

### Provisioning

For automated provisioning, clone this repository and add to your Grafana provisioning configuration:

```yaml
apiVersion: 1
providers:
  - name: 'formae'
    orgId: 1
    folder: 'formae'
    type: file
    options:
      path: /path/to/formae-grafana-dashboards/dashboards
```

## Requirements

- Grafana 10.0+
- Prometheus datasource (for metrics)
- Loki datasource (for logs)
- Formae agent with OpenTelemetry enabled

## Formae Configuration

Enable OpenTelemetry in your formae configuration:

```pkl
agent {
  oTel {
    enabled = true
    otlp {
      endpoint = "localhost:4317"
      protocol = "grpc"
      insecure = true
    }
  }
}
```

## License

BSD 3-Clause License - see [LICENSE](LICENSE) for details.
