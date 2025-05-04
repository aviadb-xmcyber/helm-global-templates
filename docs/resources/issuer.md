# Issuer

## Parameters for `issuers`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `issuers` | List of maps | Yes | A list containing Issuer configurations. Each item in the list defines an Issuer. |
| `name` | string | Yes | The name of the Issuer. |
| `disabled` | boolean | No | If true, disables the Issuer. |
| `namespace` | string | No | The namespace in which the Issuer should be created. If not provided, the release namespace will be used. |
| `namespaces` | List of strings | No | A list of namespaces in which to create the Issuer. If both `namespace` and `namespaces` are provided, `namespace` takes precedence. |
| `labels` | map | No | Custom labels for the Issuer. |
| `annotations` | map | No | Annotations for the Issuer metadata. |
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

## Example of a Simple Issuer

```yaml
issuers:
  - name: letsencrypt-staging
    namespace: cert-manager
    labels:
      app: cert-manager
    annotations:
      description: "Let's Encrypt Staging Issuer"
    acme:
      server: https://acme-staging-v02.api.letsencrypt.org/directory
      email: admin@example.com
      privateKeySecretRef:
        name: letsencrypt-staging-account-key
      solvers:
        - http01:
            ingress:
              class: nginx
```

## Example of a CA Issuer

```yaml
issuers:
  - name: ca-issuer
    namespace: cert-manager
    ca:
      secretName: ca-key-pair
```

## Example of a Self-Signed Issuer

```yaml
issuers:
  - name: selfsigned-issuer
    namespace: cert-manager
    selfSigned: {}
```