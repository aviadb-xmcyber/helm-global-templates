# Unit Tests

## Overview

This document provides comprehensive guidance for testing the Helm library chart. Our testing strategy uses the Helm Unit Test plugin to validate template rendering and ensure consistent behavior across different configurations.

## Prerequisites

### Required Tools

1. [Helm](https://helm.sh/)
2. [Helm Unit Test Plugin](https://github.com/helm-unittest/helm-unittest)

### Installation

1. Install Helm:

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

2. Install Helm Unit Test Plugin:

```bash
helm plugin install https://github.com/helm-unittest/helm-unittest.git
```

## Test Structure

The tests are organized in the following directory structure:

```
charts/
  test-chart/
    tests/
      deployment/
        deployment_test.yaml    # Test cases for deployments
        deployment_values.yaml  # Test values for deployments
      service/
        service_test.yaml      # Test cases for services
        service_values.yaml    # Test values for services
      configmap/
        configmap_test.yaml    # Test cases for configmaps
        configmap_values.yaml  # Test values for configmaps
      ...
      ...
```

## Running Tests

To run all tests:

```bash
helm unittest -f "tests/*/*_test.yaml" charts/test-chart 
```

To run tests for a specific component: (replace `deployment` with the component name)

```bash
helm unittest -f "tests/deployment/*_test.yaml" charts/test-chart 
```

## Writing Tests

### Basic Test Structure

```yaml
suite: Test deployment template
templates:
  - template.yaml
tests:
  - it: should create deployment with correct name and namespace
    values:
      - deployment_values.yaml
    asserts:
      - equal:
          path: metadata.name
          value: api
      - equal:
          path: metadata.namespace
          value: test-namespace
```

### Test Values Example

```yaml
# deployment_values.yaml
deployments:
  - name: api
    namespace: test-namespace
    containers:
      - name: api-container
        image:
          registry: docker.io
          repository: busybox
          tag: 1.0.0
```

## Additional Resources

- [Helm Unit Test Documentation](https://github.com/helm-unittest/helm-unittest?tab=readme-ov-file#documentation)
