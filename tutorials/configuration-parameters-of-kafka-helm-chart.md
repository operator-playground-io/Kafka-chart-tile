# Configuration Parameters of Kafka Helm Chart

The following tables lists the configurable parameters of the Kafka chart and their default values per section/component:

### Global parameters

| Parameter                 | Description                                     | Default                                                 |
| ------------------------- | ----------------------------------------------- | ------------------------------------------------------- |
| `global.imageRegistry`    | Global Docker image registry                    | `nil`                                                   |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]` (does not add image pull secrets to deployed pods) |
| `global.storageClass`     | Global storage class for dynamic provisioning   | `nil`                                                   |

### Common parameters

| Parameter           | Description                                       | Default                         |
| ------------------- | ------------------------------------------------- | ------------------------------- |
| `nameOverride`      | String to partially override kafka.fullname       | `nil`                           |
| `fullnameOverride`  | String to fully override kafka.fullname           | `nil`                           |
| `clusterDomain`     | Default Kubernetes cluster domain                 | `cluster.local`                 |
| `commonLabels`      | Labels to add to all deployed objects             | `{}`                            |
| `commonAnnotations` | Annotations to add to all deployed objects        | `{}`                            |
| `extraDeploy`       | Array of extra objects to deploy with the release | `nil` (evaluated as a template) |

### Kafka parameters

| Parameter                                 | Description                                                  | Default                                                 |
| ----------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------- |
| `image.registry`                          | Kafka image registry                                         | `docker.io`                                             |
| `image.repository`                        | Kafka image name                                             | `bitnami/kafka`                                         |
| `image.tag`                               | Kafka image tag                                              | `{TAG_NAME}`                                            |
| `image.pullPolicy`                        | Kafka image pull policy                                      | `IfNotPresent`                                          |
| `image.pullSecrets`                       | Specify docker-registry secret names as an array             | `[]` (does not add image pull secrets to deployed pods) |
| `image.debug`                             | Set to true if you would like to see extra information on logs | `false`                                                 |
| `config`                                  | Configuration file for Kafka. Auto-generated based on other parameters when not specified (see [below](https://github.com/bitnami/charts/blob/master/bitnami/kafka/README.md#setting-custom-parameters)) | `nil`                                                   |
| `existingConfigmap`                       | Name of existing ConfigMap with Kafka configuration (see [below](https://github.com/bitnami/charts/blob/master/bitnami/kafka/README.md#setting-custom-parameters)) | `nil`                                                   |
| `log4j`                                   | An optional log4j.properties file to overwrite the default of the Kafka brokers. | `nil`                                                   |
| `existingLog4jConfigMap`                  | The name of an existing ConfigMap containing a log4j.properties file. | `nil`                                                   |
| `heapOpts`                                | Kafka's Java Heap size                                       | `-Xmx1024m -Xms1024m`                                   |
| `deleteTopicEnable`                       | Switch to enable topic deletion or not                       | `false`                                                 |
| `autoCreateTopicsEnable`                  | Switch to enable auto creation of topics. Enabling auto creation of topics not recommended for production or similar environments | `false`                                                 |
| `logFlushIntervalMessages`                | The number of messages to accept before forcing a flush of data to disk | `10000`                                                 |
| `logFlushIntervalMs`                      | The maximum amount of time a message can sit in a log before we force a flush | `1000`                                                  |
| `logRetentionBytes`                       | A size-based retention policy for logs                       | `_1073741824`                                           |
| `logRetentionCheckIntervalMs`             | The interval at which log segments are checked to see if they can be deleted | `300000`                                                |
| `logRetentionHours`                       | The minimum age of a log file to be eligible for deletion due to age | `168`                                                   |
| `logSegmentBytes`                         | The maximum size of a log segment file. When this size is reached a new log segment will be created | `_1073741824`                                           |
| `logsDirs`                                | A comma separated list of directories under which to store log files | `/bitnami/kafka/data`                                   |
| `maxMessageBytes`                         | The largest record batch size allowed by Kafka               | `1000012`                                               |
| `defaultReplicationFactor`                | Default replication factors for automatically created topics | `1`                                                     |
| `offsetsTopicReplicationFactor`           | The replication factor for the offsets topic                 | `1`                                                     |
| `transactionStateLogReplicationFactor`    | The replication factor for the transaction topic             | `1`                                                     |
| `transactionStateLogMinIsr`               | Overridden min.insync.replicas config for the transaction topic | `1`                                                     |
| `numIoThreads`                            | The number of threads doing disk I/O                         | `8`                                                     |
| `numNetworkThreads`                       | The number of threads handling network requests              | `3`                                                     |
| `numPartitions`                           | The default number of log partitions per topic               | `1`                                                     |
| `numRecoveryThreadsPerDataDir`            | The number of threads per data directory to be used for log recovery at startup and flushing at shutdown | `1`                                                     |
| `socketReceiveBufferBytes`                | The receive buffer (SO_RCVBUF) used by the socket server     | `102400`                                                |
| `socketRequestMaxBytes`                   | The maximum size of a request that the socket server will accept (protection against OOM) | `_104857600`                                            |
| `socketSendBufferBytes`                   | The send buffer (SO_SNDBUF) used by the socket server        | `102400`                                                |
| `zookeeperConnectionTimeoutMs`            | Timeout in ms for connecting to Zookeeper                    | `6000`                                                  |
| `extraEnvVars`                            | Extra environment variables to add to kafka pods (see [below](https://github.com/bitnami/charts/blob/master/bitnami/kafka/README.md#setting-custom-parameters)) | `[]`                                                    |
| `extraVolumes`                            | Extra volume(s) to add to Kafka statefulset                  | `[]`                                                    |
| `extraVolumeMounts`                       | Extra volumeMount(s) to add to Kafka containers              | `[]`                                                    |
| `auth.clientProtocol`                     | Authentication protocol for communications with clients. Allowed protocols: `plaintext`, `tls`, `mtls`, `sasl` and `sasl_tls` | `plaintext`                                             |
| `auth.interBrokerProtocol`                | Authentication protocol for inter-broker communications. Allowed protocols: `plaintext`, `tls`, `mtls`, `sasl` and `sasl_tls` | `plaintext`                                             |
| `auth.saslMechanisms`                     | SASL mechanisms when either `auth.interBrokerProtocol` or `auth.clientProtocol` are `sasl`. Allowed types: `plain`, `scram-sha-256`, `scram-sha-512` | `plain,scram-sha-256,scram-sha-512`                     |
| `auth.saslInterBrokerMechanism`           | SASL mechanism to use as inter broker protocol, it must be included at `auth.saslMechanisms` | `plain`                                                 |
| `auth.jksSecret`                          | Name of the existing secret containing the truststore and one keystore per Kafka broker you have in the cluster | `nil`                                                   |
| `auth.jksPassword`                        | Password to access the JKS files when they are password-protected | `nil`                                                   |
| `auth.tlsEndpointIdentificationAlgorithm` | The endpoint identification algorithm to validate server hostname using server certificate | `https`                                                 |
| `auth.jaas.interBrokerUser`               | Kafka inter broker communication user for SASL authentication | `admin`                                                 |
| `auth.jaas.interBrokerPassword`           | Kafka inter broker communication password for SASL authentication | `nil`                                                   |
| `auth.jaas.zookeeperUser`                 | Kafka Zookeeper user for SASL authentication                 | `nil`                                                   |
| `auth.jaas.zookeeperPassword`             | Kafka Zookeeper password for SASL authentication             | `nil`                                                   |
| `auth.jaas.existingSecret`                | Name of the existing secret containing credentials for brokerUser, interBrokerUser and zookeeperUser | `nil`                                                   |
| `auth.jaas.clientUsers`                   | List of Kafka client users to be created, separated by commas. This values will override `auth.jaas.clientUser` | `[]`                                                    |
| `auth.jaas.clientPasswords`               | List of passwords for `auth.jaas.clientUsers`. It is mandatory to provide the passwords when using `auth.jaas.clientUsers` | `[]`                                                    |
| `listeners`                               | The address(es) the socket server listens on. Auto-calculated it's set to an empty array | `[]`                                                    |
| `advertisedListeners`                     | The address(es) (hostname:port) the broker will advertise to producers and consumers. Auto-calculated it's set to an empty array | `[]`                                                    |
| `listenerSecurityProtocolMap`             | The protocol->listener mapping. Auto-calculated it's set to nil | `nil`                                                   |
| `allowPlaintextListener`                  | Allow to use the PLAINTEXT listener                          | `true`                                                  |
| `interBrokerListenerName`                 | The listener that the brokers should communicate on          | `INTERNAL`                                              |
| `initContainers`                          | Add extra init containers                                    | `[]`                                                    |

### Statefulset parameters

| Parameter                   | Description                                                  | Default                                           |
| --------------------------- | ------------------------------------------------------------ | ------------------------------------------------- |
| `replicaCount`              | Number of Kafka nodes                                        | `1`                                               |
| `minBrokerId`               | Minimal broker.id value, nodes increment their `broker.id` respectively | `0`                                               |
| `updateStrategy`            | Update strategy for the stateful set                         | `RollingUpdate`                                   |
| `rollingUpdatePartition`    | Partition update strategy                                    | `nil`                                             |
| `podLabels`                 | Kafka pod labels                                             | `{}` (evaluated as a template)                    |
| `podAnnotations`            | Kafka Pod annotations                                        | `{}` (evaluated as a template)                    |
| `priorityClassName`         | Name of the existing priority class to be used by kafka pods | `""`                                              |
| `podAffinityPreset`         | Pod affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard` | `""`                                              |
| `podAntiAffinityPreset`     | Pod anti-affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard` | `soft`                                            |
| `nodeAffinityPreset.type`   | Node affinity preset type. Ignored if `affinity` is set. Allowed values: `soft` or `hard` | `""`                                              |
| `nodeAffinityPreset.key`    | Node label key to match Ignored if `affinity` is set.        | `""`                                              |
| `nodeAffinityPreset.values` | Node label values to match. Ignored if `affinity` is set.    | `[]`                                              |
| `affinity`                  | Affinity for pod assignment                                  | `{}` (evaluated as a template)                    |
| `nodeSelector`              | Node labels for pod assignment                               | `{}` (evaluated as a template)                    |
| `tolerations`               | Tolerations for pod assignment                               | `[]` (evaluated as a template)                    |
| `podSecurityContext`        | Kafka pods' Security Context                                 | `{}`                                              |
| `containerSecurityContext`  | Kafka containers' Security Context                           | `{}`                                              |
| `resources.limits`          | The resources limits for Kafka containers                    | `{}`                                              |
| `resources.requests`        | The requested resources for Kafka containers                 | `{}`                                              |
| `livenessProbe`             | Liveness probe configuration for Kafka                       | `Check values.yaml file`                          |
| `readinessProbe`            | Readiness probe configuration for Kafka                      | `Check values.yaml file`                          |
| `customLivenessProbe`       | Custom Liveness probe configuration for Kafka                | `{}`                                              |
| `customReadinessProbe`      | Custom Readiness probe configuration for Kafka               | `{}`                                              |
| `pdb.create`                | Enable/disable a Pod Disruption Budget creation              | `false`                                           |
| `pdb.minAvailable`          | Minimum number/percentage of pods that should remain scheduled | `nil`                                             |
| `pdb.maxUnavailable`        | Maximum number/percentage of pods that may be made unavailable | `1`                                               |
| `command`                   | Override kafka container command                             | `['/scripts/setup.sh']` (evaluated as a template) |
| `args`                      | Override kafka container arguments                           | `[]` (evaluated as a template)                    |
| `sidecars`                  | Attach additional sidecar containers to the Kafka pod        | `{}`                                              |

### Exposure parameters

| Parameter                                         | Description                                                  | Default                       |
| ------------------------------------------------- | ------------------------------------------------------------ | ----------------------------- |
| `service.type`                                    | Kubernetes Service type                                      | `ClusterIP`                   |
| `service.port`                                    | Kafka port for client connections                            | `9092`                        |
| `service.internalPort`                            | Kafka port for inter-broker connections                      | `9093`                        |
| `service.externalPort`                            | Kafka port for external connections                          | `9094`                        |
| `service.nodePorts.client`                        | Nodeport for client connections                              | `""`                          |
| `service.nodePorts.external`                      | Nodeport for external connections                            | `""`                          |
| `service.loadBalancerIP`                          | loadBalancerIP for Kafka Service                             | `nil`                         |
| `service.loadBalancerSourceRanges`                | Address(es) that are allowed when service is LoadBalancer    | `[]`                          |
| `service.annotations`                             | Service annotations                                          | `{}`(evaluated as a template) |
| `externalAccess.enabled`                          | Enable Kubernetes external cluster access to Kafka brokers   | `false`                       |
| `externalAccess.autoDiscovery.enabled`            | Enable using an init container to auto-detect external IPs/ports by querying the K8s API | `false`                       |
| `externalAccess.autoDiscovery.image.registry`     | Init container auto-discovery image registry (kubectl)       | `docker.io`                   |
| `externalAccess.autoDiscovery.image.repository`   | Init container auto-discovery image name (kubectl)           | `bitnami/kubectl`             |
| `externalAccess.autoDiscovery.image.tag`          | Init container auto-discovery image tag (kubectl)            | `{TAG_NAME}`                  |
| `externalAccess.autoDiscovery.image.pullPolicy`   | Init container auto-discovery image pull policy (kubectl)    | `Always`                      |
| `externalAccess.autoDiscovery.resources.limits`   | Init container auto-discovery resource limits                | `{}`                          |
| `externalAccess.autoDiscovery.resources.requests` | Init container auto-discovery resource requests              | `{}`                          |
| `externalAccess.service.type`                     | Kubernetes Service type for external access. It can be NodePort or LoadBalancer | `LoadBalancer`                |
| `externalAccess.service.port`                     | Kafka port used for external access when service type is LoadBalancer | `9094`                        |
| `externalAccess.service.loadBalancerIPs`          | Array of load balancer IPs for Kafka brokers                 | `[]`                          |
| `externalAccess.service.loadBalancerSourceRanges` | Address(es) that are allowed when service is LoadBalancer    | `[]`                          |
| `externalAccess.service.domain`                   | Domain or external ip used to configure Kafka external listener when service type is NodePort | `nil`                         |
| `externalAccess.service.nodePorts`                | Array of node ports used to configure Kafka external listener when service type is NodePort | `[]`                          |
| `externalAccess.service.annotations`              | Service annotations for external access                      | `{}`(evaluated as a template) |

### Persistence parameters

| Parameter                      | Description                                                  | Default                       |
| ------------------------------ | ------------------------------------------------------------ | ----------------------------- |
| `persistence.enabled`          | Enable Kafka data persistence using PVC, note that Zookeeper persistence is unaffected | `true`                        |
| `persistence.existingClaim`    | Provide an existing `PersistentVolumeClaim`, the value is evaluated as a template | `nil`                         |
| `persistence.storageClass`     | PVC Storage Class for Kafka data volume                      | `nil`                         |
| `persistence.accessMode`       | PVC Access Mode for Kafka data volume                        | `ReadWriteOnce`               |
| `persistence.size`             | PVC Storage Request for Kafka data volume                    | `8Gi`                         |
| `persistence.annotations`      | Annotations for the PVC                                      | `{}`(evaluated as a template) |
| `persistence.mountPath`        | Mount path of the Kafka data volume                          | `/bitnami/kafka`              |
| `logPersistence.enabled`       | Enable Kafka logs persistence using PVC, note that Zookeeper persistence is unaffected | `false`                       |
| `logPersistence.existingClaim` | Provide an existing `PersistentVolumeClaim`, the value is evaluated as a template | `nil`                         |
| `logPersistence.accessMode`    | PVC Access Mode for Kafka logs volume                        | `ReadWriteOnce`               |
| `logPersistence.size`          | PVC Storage Request for Kafka logs volume                    | `8Gi`                         |
| `logPersistence.annotations`   | Annotations for the PVC                                      | `{}`(evaluated as a template) |
| `logPersistence.mountPath`     | Mount path of the Kafka logs volume                          | `/opt/bitnami/kafka/logs`     |

### RBAC parameters

| Parameter               | Description                                      | Default                                       |
| ----------------------- | ------------------------------------------------ | --------------------------------------------- |
| `serviceAccount.create` | Enable creation of ServiceAccount for Kafka pods | `true`                                        |
| `serviceAccount.name`   | Name of the created serviceAccount               | Generated using the `kafka.fullname` template |
| `rbac.create`           | Weather to create & use RBAC resources or not    | `false`                                       |

### Volume Permissions parameters

| Parameter                              | Description                                                  | Default                                                 |
| -------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------- |
| `volumePermissions.enabled`            | Enable init container that changes the owner and group of the persistent volume(s) mountpoint to `runAsUser:fsGroup` | `false`                                                 |
| `volumePermissions.image.registry`     | Init container volume-permissions image registry             | `docker.io`                                             |
| `volumePermissions.image.repository`   | Init container volume-permissions image name                 | `bitnami/minideb`                                       |
| `volumePermissions.image.tag`          | Init container volume-permissions image tag                  | `buster`                                                |
| `volumePermissions.image.pullPolicy`   | Init container volume-permissions image pull policy          | `Always`                                                |
| `volumePermissions.image.pullSecrets`  | Specify docker-registry secret names as an array             | `[]` (does not add image pull secrets to deployed pods) |
| `volumePermissions.resources.limits`   | Init container volume-permissions resource limits            | `{}`                                                    |
| `volumePermissions.resources.requests` | Init container volume-permissions resource requests          | `{}`                                                    |
| `volumePermissions.securityContext`    | Init container volume-permissions security context           | `{runAsUser: 0}` (interpreted as YAML)                  |

### Metrics parameters

| Parameter                              | Description                                                  | Default                                                 |
| -------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------- |
| `metrics.kafka.enabled`                | Whether or not to create a standalone Kafka exporter to expose Kafka metrics | `false`                                                 |
| `metrics.kafka.image.registry`         | Kafka exporter image registry                                | `docker.io`                                             |
| `metrics.kafka.image.repository`       | Kafka exporter image name                                    | `bitnami/kafka-exporter`                                |
| `metrics.kafka.image.tag`              | Kafka exporter image tag                                     | `{TAG_NAME}`                                            |
| `metrics.kafka.image.pullPolicy`       | Kafka exporter image pull policy                             | `IfNotPresent`                                          |
| `metrics.kafka.image.pullSecrets`      | Specify docker-registry secret names as an array             | `[]` (does not add image pull secrets to deployed pods) |
| `metrics.kafka.extraFlags`             | Extra flags to be passed to Kafka exporter                   | `{}`                                                    |
| `metrics.kafka.certificatesSecret`     | Name of the existing secret containing the optional certificate and key files | `nil`                                                   |
| `metrics.kafka.resources.limits`       | Kafka Exporter container resource limits                     | `{}`                                                    |
| `metrics.kafka.resources.requests`     | Kafka Exporter container resource requests                   | `{}`                                                    |
| `metrics.kafka.service.type`           | Kubernetes service type (`ClusterIP`, `NodePort` or `LoadBalancer`) for Kafka Exporter | `ClusterIP`                                             |
| `metrics.kafka.service.port`           | Kafka Exporter Prometheus port                               | `9308`                                                  |
| `metrics.kafka.service.nodePort`       | Kubernetes HTTP node port                                    | `""`                                                    |
| `metrics.kafka.service.annotations`    | Annotations for Prometheus metrics service                   | `Check values.yaml file`                                |
| `metrics.kafka.service.loadBalancerIP` | loadBalancerIP if service type is `LoadBalancer`             | `nil`                                                   |
| `metrics.kafka.service.clusterIP`      | Static clusterIP or None for headless services               | `nil`                                                   |
| `metrics.jmx.enabled`                  | Whether or not to expose JMX metrics to Prometheus           | `false`                                                 |
| `metrics.jmx.image.registry`           | JMX exporter image registry                                  | `docker.io`                                             |
| `metrics.jmx.image.repository`         | JMX exporter image name                                      | `bitnami/jmx-exporter`                                  |
| `metrics.jmx.image.tag`                | JMX exporter image tag                                       | `{TAG_NAME}`                                            |
| `metrics.jmx.image.pullPolicy`         | JMX exporter image pull policy                               | `IfNotPresent`                                          |
| `metrics.jmx.image.pullSecrets`        | Specify docker-registry secret names as an array             | `[]` (does not add image pull secrets to deployed pods) |
| `metrics.jmx.resources.limits`         | JMX Exporter container resource limits                       | `{}`                                                    |
| `metrics.jmx.resources.requests`       | JMX Exporter container resource requests                     | `{}`                                                    |
| `metrics.jmx.service.type`             | Kubernetes service type (`ClusterIP`, `NodePort` or `LoadBalancer`) for JMX Exporter | `ClusterIP`                                             |
| `metrics.jmx.service.port`             | JMX Exporter Prometheus port                                 | `5556`                                                  |
| `metrics.jmx.service.nodePort`         | Kubernetes HTTP node port                                    | `""`                                                    |
| `metrics.jmx.service.annotations`      | Annotations for Prometheus metrics service                   | `Check values.yaml file`                                |
| `metrics.jmx.service.loadBalancerIP`   | loadBalancerIP if service type is `LoadBalancer`             | `nil`                                                   |
| `metrics.jmx.service.clusterIP`        | Static clusterIP or None for headless services               | `nil`                                                   |
| `metrics.jmx.whitelistObjectNames`     | Allows setting which JMX objects you want to expose to via JMX stats to JMX Exporter | (see `values.yaml`)                                     |
| `metrics.jmx.config`                   | Configuration file for JMX exporter                          | (see `values.yaml`)                                     |
| `metrics.jmx.existingConfigmap`        | Name of existing ConfigMap with JMX exporter configuration   | `nil`                                                   |
| `metrics.serviceMonitor.enabled`       | if `true`, creates a Prometheus Operator ServiceMonitor (requires `metrics.kafka.enabled` or `metrics.jmx.enabled` to be `true`) | `false`                                                 |
| `metrics.serviceMonitor.namespace`     | Namespace which Prometheus is running in                     | `monitoring`                                            |
| `metrics.serviceMonitor.interval`      | Interval at which metrics should be scraped                  | `nil`                                                   |
| `metrics.serviceMonitor.scrapeTimeout` | Timeout after which the scrape is ended                      | `nil` (Prometheus Operator default value)               |
| `metrics.serviceMonitor.selector`      | ServiceMonitor selector labels                               | `nil` (Prometheus Operator default value)               |

### Zookeeper chart parameters

| Parameter                       | Description                                          | Default |
| ------------------------------- | ---------------------------------------------------- | ------- |
| `zookeeper.enabled`             | Switch to enable or disable the Zookeeper helm chart | `true`  |
| `zookeeper.persistence.enabled` | Enable Zookeeper persistence using PVC               | `true`  |
| `externalZookeeper.servers`     | Server or list of external Zookeeper servers to use  | `[]`    |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```
helm install my-release \
  --set replicaCount=3 \
  bitnami/kafka
```

The above command deploys Kafka with 3 brokers (replicas).

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```
helm install my-release -f values.yaml bitnami/kafka
```

 **NOTE :** For more details refer to [Kafka](https://github.com/bitnami/charts/tree/master/bitnami/kafka).