# Certificate

## Parameters for `certificates`

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `certificates` | List of maps | Yes | A list containing Certificate configurations. Each item in the list defines a Certificate. |
| `name` | string | Yes | The name of the Certificate. |
| `disabled` | boolean | No | If true, disables the Certificate. |
| `secretName` | string | Yes | The name of the Secret resource that will be created by cert-manager to store the certificate. |
| `namespace` | string | No | The namespace in which the Certificate should be created. If not provided, the release namespace will be used. |
| `namespaces` | List of strings | No | A list of namespaces in which to create the Certificate. If both `namespace` and `namespaces` are provided, `namespace` takes precedence. |
| `labels` | map | No | Custom labels for the Certificate. |
| `annotations` | map | No | Annotations for the Certificate metadata. |
| `duration` | string | No | The requested duration of the certificate. Defaults to `2160h` (90 days) if not specified. |
| `renewBefore` | string | No | The amount of time before the certificate expiry to attempt renewal. Defaults to `720h` (30 days) if not specified. |
| `subject` | map | No | The subject of the certificate. |
| `privateKey` | map | No | Configuration for the certificate's private key. |
| `privateKey.algorithm` | string | No | The algorithm for the private key. |
| `privateKey.encoding` | string | No | The encoding for the private key. |
| `privateKey.size` | integer | No | The size of the private key. Defaults to `2048` if not specified. |
| `privateKey.rotationPolicy` | string | No | The rotation policy for the private key. Defaults to `Never` if not specified. |
| `dnsNames` | List of strings | No | A list of DNS names to include in the certificate. |
| `ipAddresses` | List of strings | No | A list of IP addresses to include in the certificate. |
| `uris` | List of strings | No | A list of URIs to include in the certificate. |
| `emailAddresses` | List of strings | No | A list of email addresses to include in the certificate. |
| `issuerRef` | map | Yes | Reference to the issuer that will be used to issue the certificate. |
| `issuerRef.name` | string | Yes | The name of the issuer. |
| `issuerRef.kind` | string | No | The kind of the issuer. |
| `issuerRef.group` | string | No | The group of the issuer. |
| `keystores` | map | No | Configuration for additional keystore formats. |
| `secretTemplate` | map | No | Template for customizing the generated Secret resource. |
| `isCA` | boolean | No | Whether this certificate should be its own Certificate Authority. |
| `usages` | List of strings | No | The usages of the certificate. |
| `commonName` | string | No | The common name to be used in the certificate. |

## Example of a Simple Certificate

```yaml
certificates:
  - name: example-certificate
    secretName: example-tls-secret
    namespace: my-namespace
    labels:
      app: my-app
    annotations:
      description: "This is an example Certificate"
    duration: "2160h"
    renewBefore: "720h"
    privateKey:
      algorithm: RSA
      encoding: PKCS1
      size: 2048
      rotationPolicy: Never
    dnsNames:
      - example.com
      - www.example.com
    issuerRef:
      name: letsencrypt-prod
      kind: ClusterIssuer
      group: cert-manager.io
    commonName: example.com
```