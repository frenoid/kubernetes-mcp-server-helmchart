# Kubernetes MCP Server helm chart
Deploy the [Kubernetes MCP Server](https://github.com/containers/kubernetes-mcp-server/tree/main) onto your cluster with this Helm Chart

## Prerequisites
- Kubernetes >= 1.24
- Helm >= 3.9

## Installing
Clone the repo
```bash
git clone git@github.com:frenoid/kubernetes-mcp-server-helmchart.git
```

Enter the directory
```bash
cd kubernetes-mcp-server
```

Deploy the chart as `myrelease`
```bash
 helm install myrelease . -f values.yaml
```

## Uninstalling
Uninstall the `myrelease` deployment using
```bash
helm uninstall myrelease
```
The command deletes the release named `myrelease` and frees all the kubernetes resources associated with the release.

**TIP**: Specify the `--purge` argument to the above command to remove the release from the store and make its name free for later use.

## Configuration

### Global parameters

| Name                      | Description                                     | Default |
| ------------------------- | ----------------------------------------------- | ------- |
| `global.imageRegistry`    | Global Docker image registry                    | `""`    |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]`    |

### Common parameters

| Name                | Description                                                                                         | Default |
| ------------------- | --------------------------------------------------------------------------------------------------- | ------- |
| `kubeVersion`       | Override Kubernetes version                                                                         | `""`    |
| `nameOverride`      | Partially override `kubernetes-mcp.fullname` template with a string (will prepend the release name) | `""`    |
| `fullnameOverride`  | Fully override `kubernetes-mcp.fullname` template with a string                                     | `""`    |
| `namespaceOverride` | Fully override `common.names.namespace` template with a string                                      | `""`    |
| `commonAnnotations` | Annotations to add to all deployed objects                                                          | `{}`    |
| `commonLabels`      | Labels to add to all deployed objects                                                               | `{}`    |
| `extraDeploy`       | Array of extra objects to deploy with the release                                                   | `[]`    |

### Parameters

| Name                                       | Description                                                                                                | Default                        |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------- | ------------------------------ |
| `enableWriteDelete`                        | Adds Create, Patch, Update, and Delete permissions to the MCP server                                       | `false`                        |
| `replicaCount`                             | Number of replicas                                                                                         | `1`                            |
| `image.repository`                         | Image repository                                                                                           | `docker.io/frenoid/kubernetes-mcp-server` |
| `image.tag`                                | Image tag                                                                                                  | `v0.0.53`                      |
| `image.pullPolicy`                         | Image pull policy                                                                                          | `IfNotPresent`                 |
| `serviceAccount.create`                    | Specifies whether a service account should be created                                                      | `true`                         |
| `serviceAccount.annotations`               | Service account annotations                                                                                | `{}`                           |
| `serviceAccount.name`                      | The name of the service account to use (Generated using the `kubernetes-mcp.fullname` template if not set) | `kubernetes-mcp-server`        | 
| `serviceAccount.automount`                 | Indicates whether to automatically mount a ServiceAccount's API credentials                                | `false`                        |
| `deploymentAnnotations`                    | Additional deployment annotations                                                                          | `{}`                           |
| `podAnnotations`                           | Additional pod annotations                                                                                 | `{}`                           |
| `podLabels`                                | Additional pod labels                                                                                      | `{}`                           |
| `podSecurityContext`                       | Pod security context                                                                                       |                                |
| `podSecurityContext.seccompProfile.type`   | Set pod's Security Context seccomp profile                                                                 | `RuntimeDefault`               |
| `priorityClassName`                        | Priority class name                                                                                        | `nil`                          |
| `runtimeClassName`                         | Runtime class name                                                                                         | `""`                           |
| `securityContext`                          | Container security context                                                                                 |                                |
| `securityContext.allowPrivilegeEscalation` | Set container's Security Context allowPrivilegeEscalation                                                  | `false`                        |
| `securityContext.capabilities.drop`        | List of capabilities to be dropped                                                                         | `["ALL"]`                      |
| `securityContext.readOnlyRootFilesystem`   | Set container's Security Context readOnlyRootFilesystem                                                    | `true`                         |
| `securityContext.runAsNonRoot`             | Whether the container must run as a non-root user                                                          | `true`                         |
| `securityContext.runAsUser`                | The UID to run the entrypoint of the container process                                                     | `65534`                        |
| `securityContext.runAsGroup`               | The GID to run the entrypoint of the container process                                                     | `65534`                        |
| `containerPorts.http`                      | Container port for HTTP                                                                                    | `8080`                         |
| `service.annotations`                      | Service annotations                                                                                        | `{}`                           |
| `service.type`                             | Service type                                                                                               | `ClusterIP`                    |
| `service.clusterIP`                        | Static cluster IP address or None for headless service when service type is ClusterIP                      | `nil`                          |
| `service.loadBalancerIP`                   | Static load balancer IP address when service type is LoadBalancer                                          | `nil`                          |
| `service.loadBalancerSourceRanges`         | Source IP address ranges when service type is LoadBalancer                                                 | `nil`                          |
| `service.externalTrafficPolicy`            | External traffic routing policy when service type is LoadBalancer or NodePort                              | `Cluster`                      |
| `service.ports.http`                       | Service port for HTTP                                                                                      | `8080`                         |
| `service.nodePorts.http`                   | Service node port for HTTP when service type is LoadBalancer or NodePort                                   | `nil`                          |
| `ingress.enabled`                          | Enable ingress controller resource                                                                         | `false`                        |
| `ingress.ingressClassName`                 | IngressClass that will be be used to implement the Ingress                                                 | `""`                           |
| `ingress.pathType`                         | Ingress path type                                                                                          | `ImplementationSpecific`       |
| `ingress.annotations`                      | Ingress annotations                                                                                        | `{}`                           |
| `ingress.hosts[0].host`                    | Hostname to your Kubernetes MCP Server installation                                                        | `kubernetes-mcp.local`         |
| `ingress.hosts[0].paths`                   | Paths within the url structure                                                                             | `["/"]`                        |
| `ingress.tls`                              | TLS configuration                                                                                          | `[]`                           |
| `resources`                                | CPU/Memory resource requests/limits                                                                        | `{}`                           |
| `nodeSelector`                             | Node labels for pod assignment                                                                             | `{}`                           |
| `tolerations`                              | Tolerations for pod assignment                                                                             | `[]`                           |
| `affinity`                                 | Map of node/pod affinities                                                                                 | `{}`                           |
| `extraArgs`                                | Additional container arguments                                                                             | `{}`                           |
| `extraEnvVars`                             | Additional container environment variables                                                                 | `[]`                           |
| `extraEnvVarsCM`                           | Name of existing ConfigMap containing additional container environment variables                           | `nil`                          |
| `extraEnvVarsSecret`                       | Name of existing Secret containing additional container environment variables                              | `nil`                          |
| `extraVolumes`                             | Optionally specify extra list of additional volumes                                                        | `[]`                           |
| `extraVolumeMounts`                        | Optionally specify extra list of additional volumeMounts                                                   | `[]`                           |

## Setting parameters

Specify the parameters you which to customize using the `--set` argument to the `helm install` command. For instance,

```bash
$ helm install myrelease \
    --set nameOverride=my-name .
```

The above command sets the `nameOverride` to `my-name`.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```bash
$ helm install myrelease \
    --values values.yaml .
```

**TIP**: You can use the default [values.yaml](values.yaml).