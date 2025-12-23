# Formae Grafana Dashboards

Open source Grafana dashboards for monitoring [Formae](https://github.com/platform-engineering-labs/formae) infrastructure-as-code agents.

## Dashboards

| Dashboard | Description |
|-----------|-------------|
| [Formae Overview](dashboards/formae-overview.json) | Go runtime metrics, database performance |

## Installation

### Option 1: Manual Import

1. Open Grafana
2. Go to Dashboards → Import
3. Upload or paste the JSON from the `dashboards/` directory

### Option 2: Provisioning

Add to your Grafana provisioning configuration:

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

### Option 3: With LGTM Stack

If using the companion [lgtm-stack](../lgtm-stack), dashboards are automatically provisioned.

## Requirements

- Grafana 10.0+
- Prometheus data source
- Formae agent with OTel enabled

## Formae Configuration

Enable OTel in your formae configuration:

```pkl
agent {
  oTel {
    enabled = true
    serviceName = "formae-agent"
    otlp {
      endpoint = "localhost:4317"
      protocol = "grpc"
      insecure = true
    }
  }
}
```

## License

Apache 2.0
