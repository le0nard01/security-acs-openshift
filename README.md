## Repository Layout

- `acs/infrastructure/`: base ACS manifests used to deploy or size core ACS components, such as Central.
- `loki-clf/infrastructure/`: base infrastructure manifests used by the logging examples.
- `loki-clf/clf.yaml`: ClusterLogForwarder configuration for forwarding Kubernetes audit events.
- `acs/tailoredprofile/`: Compliance Operator tailored profiles and custom rules.
- `acs/stackrox-mcp/`: Helm chart for deploying the StackRox MCP integration.

## Audit Log Forwarding

`loki-clf/clf.yaml` defines a `ClusterLogForwarder` that forwards Kubernetes audit logs to Loki. It includes a `kubeAPIAudit` filter for `pods/exec` events at `RequestResponse` level, which helps capture Pod Exec activity for investigation and detection workflows.

## Compliance Custom Rule

`acs/tailoredprofile/customrule2-nist-ac-6/nist-ac-6-CR.yaml` defines a Compliance Operator `CustomRule` for NIST AC-6 least privilege validation.

The rule checks Deployments only in namespaces labeled:

```yaml
type: workload
```

For those workloads, every container must explicitly set:

```yaml
securityContext:
  runAsNonRoot: true
```

The same folder also includes sample manifests:

- `violation.yaml`: creates a workload that should fail the rule.
- `no-violation.yaml`: creates a workload that should pass the rule.
