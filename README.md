# CronJob Annotator Helm Chart

This Helm chart creates a Kubernetes CronJob that periodically re-applies annotations to specified resources. This is particularly useful for ensuring that annotations are consistently applied, such as for Velero backups.

## Prerequisites

- Kubernetes 1.12+
- Helm 3.0+

## Installation

1. Clone the repository:
    ```sh
    git clone https://github.com/your-username/cronjob-annotator.git
    cd cronjob-annotator
    ```

2. Customize the `values.yaml` file as needed to specify your targets and annotations.

3. Install the Helm chart:
    ```sh
    helm install my-annotator .
    ```

## Configuration

The following table lists the configurable parameters of the CronJob Annotator chart and their default values.

| Parameter         | Description                                                   | Default                           |
|-------------------|---------------------------------------------------------------|-----------------------------------|
| `cronjob.name`    | Name of the CronJob                                           | `annotate-resources`              |
| `cronjob.schedule`| Cron schedule expression                                      | `"*/5 * * * *"`                   |
| `cronjob.image`   | Docker image to use for the CronJob                           | `bitnami/kubectl:latest`          |
| `targets`         | List of target resources to annotate                          | See `values.yaml`                 |
| `targets.kind`    | The kind of the Kubernetes resource (e.g., `deployment`)      |                                   |
| `targets.name`    | The name of the Kubernetes resource                           |                                   |
| `targets.key`     | The annotation key to apply                                   |                                   |
| `targets.value`   | The annotation value to apply                                 |                                   |

### Example

Here is an example `values.yaml` configuration:

```yaml
cronjob:
  name: annotate-resources
  schedule: "*/5 * * * *"
  image: bitnami/kubectl:latest

targets:
  - kind: deployment
    name: my-deployment-1
    key: example.com/annotation1
    value: value1
  - kind: deployment
    name: my-deployment-2
    key: example.com/annotation2
    value: value2
```
