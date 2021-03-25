---
title: Uninstall Kafka Helm chart 
description: Learn how to uninstall Kafka Helm chart?
---

### Uninstall Kafka Helm Chart

**Step 1: Check your deployed Kafka Helm Chart.**

```execute
 helm list -n kafka
```

Output will be similar as shown below:

```output
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
my-release      kafka           1               2021-01-06 22:12:07.138654803 -0600 CST deployed        kafka-12.5.0    2.7.0
```

**Step 2: To uninstall the Kafka Helm Chart, use the helm delete command.**

```execute
helm delete my-release -n kafka
```

You should see the below output.

```output
release "my-release" uninstalled
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

**Step 3: Now, check the status of Kafka Helm chart.**

```execute
helm status my-release -n kafka
```

This should produce the below output.

```
Error: release: not found
```

### Cleanup other resources

**Step 1: To remove the `testclient` Pod, execute the below kubectl command.**

```execute
kubectl -n kafka delete -f testclient.yaml
```

The output should display as below.

```output
pod "testclient" deleted
```

**Step 2: To remove the PVCs created, execute the below kubectl delete commands.**

```execute
kubectl -n kafka delete pvc/data-my-release-kafka-0
```

```execute
kubectl -n kafka delete pvc/data-my-release-zookeeper-0
```

Refer the output shown below.

```output
persistentvolumeclaim "data-my-release-kafka-0" deleted
persistentvolumeclaim "data-my-release-zookeeper-0" deleted
```

### Conclusion

You’re done. The Kafka release and associated resources have been deleted successfully.