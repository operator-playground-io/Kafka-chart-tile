---
title: How to Uninstall Kafka Helm chart 
description: This tutorial explains how to Uninstall Kafka helm chart
---

# Uninstall Kafka Helm Chart

Check your deployed Kafka helm chart:

```execute
 helm list -n kafka
```

 Output will be similar:

```output
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
my-release      kafka           1               2021-01-06 22:12:07.138654803 -0600 CST deployed        kafka-12.5.0    2.7.0
```

To uninstall the Kafka helm chart, use the helm delete command:

```execute
helm delete my-release -n kafka
```

Output:

```output
release "my-release" uninstalled
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

```execute
helm status my-release -n kafka
```

Output:

```
Status: UNINSTALLED
```

### Cleanup other resources

To delete the `testclient` Pod, execute the below command:

```execute
kubectl -n kafka delete -f testclient.yaml
```

Output:

```output
pod "testclient" deleted
```

To delete the PVCs created, execute the below commands:

```execute
kubectl -n kafka delete pvc/data-my-release-kafka-0
```

```execute
kubectl -n kafka delete pvc/data-my-release-zookeeper-0
```

Output:

```output
persistentvolumeclaim "data-my-release-kafka-0" deleted
persistentvolumeclaim "data-my-release-zookeeper-0" deleted
```
