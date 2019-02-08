# Sealed Secrets Terraform module
Terraform module to deploy [sealed-secrets] in k8s on GCP.  
Module uses [stable/sealed-secrets] chart.

## Configuration
If you want to customize below settings provide `values.yaml` to this module.

|                 Parameter | Description                                                              | Default                                     |
| ------------------------: | :----------------------------------------------------------------------- | :------------------------------------------ |
|           **rbac.create** | `true` if rbac resources should be created                               | `true`                                      |
| **serviceAccount.create** | Whether to create a service account or not                               | `true`                                      |
|   **serviceAccount.name** | The name of the service account to create or use                         | `"sealed-secrets-controller"`               |
|            **secretName** | The name of the TLS secret containing the key used to encrypt secrets    | `"sealed-secrets-key"`                      |
|             **image.tag** | The `Sealed Secrets` image tag                                           | `v0.7.0`                                    |
|      **image.pullPolicy** | The image pull policy for the deployment                                 | `IfNotPresent`                              |
|      **image.repository** | The repository to get the controller image from                          | `quay.io/bitnami/sealed-secrets-controller` |
|             **resources** | CPU/Memory resource requests/limits                                      | `{}`                                        |
|              **crd.keep** | `true` if the sealed secret CRD should be kept when the chart is deleted | `true`                                      |

- In the case that `serviceAccount.create` is `false` and **rbac.create** is `true` it is expected for a service account with the name `serviceAccount.name` to exist _in the same namespace as this chart_ before installation.
- If `serviceAccount.create` is `true` there cannot be an existing service account with the name `serviceAccount.name`.
- If a secret with name `secretName` does not exist _in the same namespace as this chart_, then on install one will be created. If a secret already exists with this name the keys inside will be used.

---
For more information about chart and its configuration see [stable/sealed-secrets]

[sealed-secrets]: https://github.com/bitnami-labs/sealed-secrets
[stable/sealed-secrets]: https://github.com/helm/charts/tree/master/stable/sealed-secrets