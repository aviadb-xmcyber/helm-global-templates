# Namespace

## Parameters for `namespaces`

| Parameter    | Type            | Required | Description                                                                                                      |
| ------------ | --------------- | -------- | ---------------------------------------------------------------------------------------------------------------- |
| `namespaces` | List of strings | Yes      | A list containing Namespace names. Each item in the list defines a Namespace.                                    |
| `labels`     | map             | No       | Custom labels for the Namespace. Labels are automatically added with the name prefix based on the global values. |

## Example of a Simple Namespace

```yaml
namespaces:
  - my-namespace
```
