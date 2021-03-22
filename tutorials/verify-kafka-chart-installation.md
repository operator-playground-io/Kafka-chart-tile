---
title: Verify Kafka Chart Installation
description: This tutorial explains how to verify that Kafka chart installed successfully
---


Once the helm chart installation is complete, you need to verify that all the pods and services are up and running.

### Check the Status of Pods 

- Execute the following command to know the status of pods inside the namespace `kafka`:

```execute
kubectl get pods --namespace kafka
```

You will see the output like this.

```
NAME                     READY   STATUS              RESTARTS   AGE
my-release-kafka-0       0/1     ContainerCreating   0          16s
my-release-zookeeper-0   0/1     ContainerCreating   0          16s
```

It may take few minutes to change the `STATUS` from `ContainerCreating` to `Running`. 

```output
NAME                     READY   STATUS    RESTARTS   AGE
my-release-kafka-0       1/1     Running   0          60s
my-release-zookeeper-0   1/1     Running   0          60s
```

Once the `kafka` and `zookeeper` PODs are up and running , and `READY` states are `1/1` for both, your Kafka is ready to use.

### Check the Status of Kubernetes Resources

- You can execute the following command to know status of all the deployed resources inside the namespace `kafka`:


```execute
kubectl get all --namespace kafka
```

Ensure that the STATUS value of pods should be `Running` and `READY` state for each should be `1/1`.

```
NAME                         READY   STATUS    RESTARTS   AGE
pod/my-release-kafka-0       1/1     Running   0          65m
pod/my-release-zookeeper-0   1/1     Running   0          65m

NAME                                    TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
service/my-release-kafka                ClusterIP   10.111.86.138   <none>        9092/TCP                     65m
service/my-release-kafka-headless       ClusterIP   None            <none>        9092/TCP,9093/TCP            65m
service/my-release-zookeeper            ClusterIP   10.111.159.94   <none>        2181/TCP,2888/TCP,3888/TCP   65m
service/my-release-zookeeper-headless   ClusterIP   None            <none>        2181/TCP,2888/TCP,3888/TCP   65m

NAME                                    READY   AGE
statefulset.apps/my-release-kafka       1/1     65m
statefulset.apps/my-release-zookeeper   1/1     65m
```

### Conclusion

This way, you can easily verify the configuration status of Kafka pods and other deployed resources.