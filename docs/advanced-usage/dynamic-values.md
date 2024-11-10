# Dynamic Values

We tackle a common problem in our charts, where we need to generate values dynamically based on the values provided to the chart.
Typically, we could use a values file to define the values, but sometimes we need to generate values based on the provided values.
We could use a `tpl` functions to generate the values, but this can get messy and hard to maintain.

We solved this problem by using a `dynamic-values`, basically a utilily function that allows us to "inject" global values into other values.

### Usage

The syntax for injecting a global value is `{{global.<key>}}`.

> Note: You can't use dynamic-values in any resource, here is a list of properties and resources that support dynamic-values:
>
> - env values in containers (deployments, statefulsets, etc.)
> - namespaces name in all resources
> - `clusterexternalsecrets.data[].remoteRef.key`
> - `clustersecretstores.name`
> - `clustersecretstores.aws.region`
> - `externalsecrets.secretStoreRef.name`
> - `externalsecrets.data[].remoteRef.key`
> - `ingresses.rules[].host`
> - `scaledobjects.triggers[].metadata{}`
>
> If you want to use dynamic-values in other resources, please open an issue and we will add support for it.

### Example

```yaml
# Dynamic values has to be defined in the global scope
global:
  key: injected

deployments:
  - name: app
    namespace: default
    containers:
      - name: app
        image:
          registry: docker.io
          repository: busybox
          tag: latest
        ports:
          - containerPort: 8080
        env:
          - name: INJECTED_WORD
            value: "This is going to be {{ global.key }} here" # Inject the key here
```

In the example above, the value of `INJECTED_WORD` will be `This is going to be injected here`.
