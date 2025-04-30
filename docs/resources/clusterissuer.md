# ClusterIssuer

## Parameters for `clusterissuers`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `clusterissuers` | List of maps | Yes | A list containing ClusterIssuer configurations. Each item in the list defines a ClusterIssuer. |
| `name` | string | Yes | The name of the ClusterIssuer. |
| `disabled` | boolean | No | If true, disables the ClusterIssuer. |
| `labels` | map | No | Custom labels for the ClusterIssuer. |
| `annotations` | map | No | Annotations for the ClusterIssuer metadata. |
| `acme` | map | No | Configuration for ACME issuers (Let's Encrypt). |
| `acme.server` | string | No | The ACME server URL. |
| `acme.email` | string | No | The email address used for ACME registration. |
| `acme.privateKeySecretRef.name` | string | Yes (if using ACME) | The name of the secret containing the ACME account private key. |
| `acme.solvers` | List of maps | No | Configuration for ACME challenge solvers. |
| `ca` | map | No | Configuration for CA issuers. |
| `ca.secretName` | string | Yes (if using CA) | The name of the secret containing the CA certificate and key. |
| `ca.crlDistributionPoints` | List of strings | No | The CRL distribution points for the CA issuer. |
| `selfSigned` | map | No | Configuration for self-signed issuers. |
| `vault` | map | No | Configuration for HashiCorp Vault issuers. |
| `venafi` | map | No | Configuration for Venafi issuers. |

## Example of a Simple ClusterIssuer

```yaml
clusterissuers:
  - name: letsencrypt-prod
    labels:
      app: cert-manager
    annotations:
      description: "Let's Encrypt Production ClusterIssuer"
    acme:
      server: https://acme-v02.api.letsencrypt.org/directory
      email: admin@example.com
      privateKeySecretRef:
        name: letsencrypt-prod-account-key
      solvers:
        - http01:
            ingress:
              class: nginx
```

## Example of a CA ClusterIssuer

```yaml
clusterissuers:
  - name: ca-cluster-issuer
    ca:
      secretName: ca-key-pair
```

## Example of a Self-Signed ClusterIssuer

```yaml
clusterissuers:
  - name: selfsigned-cluster-issuer
    selfSigned: {}
```