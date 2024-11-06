# Image Directory

The `image-directory` pattern is a way to define a set of images in a single values file, and then reference them across multiple charts in a consistent way.

### Values File Example

Define your images in the `values.yaml` file, in this example we define two images, `busybox` and `nginx`:

```yaml
global:
  images:
    busybox: # key for the image
      registry: docker.io
      repository: busybox
      tag: 1.0.0
      # We can use digest, if provided it will be used instead of tag
      #sha: sha256:1ff6c18fbef2045af6b9c16bf034cc421a29027b800e4f9b68ae9b1cb3e9ae07

    nginx:
      registry: docker.io
      repository: nginx
      tag: 1.0.0
```

### Usage

In your chart / subchart you can point to the image by using the `imageKey` property.
Let's say we have a Deployment that uses the `busybox` image:

```yaml
deployments:
  - name: example
    namespace: default
    replicas: 1
    containers:
      - name: example
        imageKey: busybox # reference to the image key
        ports:
          - containerPort: 3000
```

### Why use this pattern?

### Why use this pattern?

- **Simplicity**: Without this pattern you would need to override the image in each deployment, in each chart, good luck with that.
- **Continuous Deployment (CD)**: When using an ArgoCD or FluxCD, you can point to a single values file that contains all the images, and then update the images in a single place.
- **Override YAML anchors**: You can't override YAML anchors ([See issue](https://github.com/helm/helm/issues/2336#issuecomment-297839969)). This pattern allows a nice workaround for this issue.
