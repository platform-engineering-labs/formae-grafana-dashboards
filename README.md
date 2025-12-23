# Formae Grafana Dashboards

Pre-built Grafana dashboards for monitoring [Formae](https://github.com/platform-engineering-labs/formae) infrastructure.

## Dashboards

### Formae Overview

A comprehensive dashboard for monitoring the Formae agent:

| Section | Metrics |
|---------|---------|
| **Formae Stats** | Stacks, targets, managed/unmanaged resources, clients, agent uptime, errors, commands |
| **Host Metrics** | CPU, memory, network I/O, disk I/O |
| **Process** | Agent CPU and memory usage |
| **Go Runtime** | Goroutines, GC, memory allocation |
| **Ergo Metrics** | Actor system health (node, processes, network) |
| **Database** | Connection pool and query performance |
| **Logs** | Application logs with level filtering |

## Installation

### Manual Import

1. Download `dashboards/formae-overview.json` from this repository
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
    folder: 'Formae'
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

Enable OpenTelemetry in your Formae configuration:

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
