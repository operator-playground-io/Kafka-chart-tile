---
title: How to Upgrade and Rollback Kafka chart 
description: This tutorial explains how to Upgrade and Rollback Kafka helm chart
---



# Upgrading Kafka

It is also important to keep Kafka helm chart updated. 

To Upgrade kafka helm chart,please execute following steps:

**Step 1:** To list all of your current releases in namespace "kafka", run the following command :

```execute
helm list -n kafka
```
You should get output similar to this:

Output:
```
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
my-release      kafka           1               2021-01-09 12:29:50.150704347 -0600 CST deployed        kafka-12.5.0    2.7.0  
```

As you can see from the output, our current Kafka (my-release) version is 2.7.0 (app version), while the chart version is 12.5.0 which is the latest one.
But suppose your current helm chart version is 12.4.0 and app version is 2.6.0 and is not updated one and you need to upgrade it. 

You need to follow below steps.

**Step 2:** Update your Helm repositories with following command :

```execute
helm repo update 
```

You can expect the following output:

```output
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "fluxcd" chart repository
...Successfully got an update from the "bitnami" chart repository
Update Complete. ⎈ Happy Helming!⎈
```

**Step 3:** Check if there’s a newer version of the Kafka chart available using following command:

```execute
helm search repo kafka --versions
```

You should see output similar to this:

```
NAME            CHART VERSION   APP VERSION     DESCRIPTION
bitnami/kafka   12.5.0          2.7.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.4.3          2.7.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.4.2          2.7.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.4.1          2.7.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.4.0          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.3.2          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.3.1          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.3.0          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.2.4          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.2.3          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.2.2          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.2.1          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.2.0          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.1.0          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   12.0.0          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.8.9          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.8.8          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.8.7          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.8.6          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.8.5          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.8.4          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.8.3          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.8.2          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.8.1          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.8.0          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.7.3          2.6.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.7.2          2.5.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.7.1          2.5.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.7.0          2.5.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.6.6          2.5.0           Apache Kafka is a distributed streaming platform.
bitnami/kafka   11.6.5          2.5.0           Apache Kafka is a distributed streaming platform.
```

As you can see from the output, there’s a new chart available (version 12.5.0) with Kafka 2.7.0 (app version). 

**Step 4:** To upgrade your Kafka release to the latest Kafka chart, execute below command:

```execute
helm upgrade my-release bitnami/kafka --namespace kafka
```

This command will produce output very similar to the output produced by helm install:

```output
Release "my-release" has been upgraded. Happy Helming!
NAME: my-release
LAST DEPLOYED: Sat Jan  9 12:45:13 2021
NAMESPACE: kafka
STATUS: deployed
REVISION: 2
TEST SUITE: None
NOTES:
** Please be patient while the chart is being deployed **

Kafka can be accessed by consumers via port 9092 on the following DNS name from within your cluster:

    my-release-kafka.kafka.svc.cluster.local

Each Kafka broker can be accessed by producers via port 9092 on the following DNS name(s) from within your cluster:

    my-release-kafka-0.my-release-kafka-headless.kafka.svc.cluster.local:9092

To create a pod that you can use as a Kafka client run the following commands:

    kubectl run my-release-kafka-client --restart='Never' --image docker.io/bitnami/kafka:2.7.0-debian-10-r1 --namespace kafka --command -- sleep infinity
    kubectl exec --tty -i my-release-kafka-client --namespace kafka -- bash

    PRODUCER:
        kafka-console-producer.sh \

            --broker-list my-release-kafka-0.my-release-kafka-headless.kafka.svc.cluster.local:9092 \
            --topic test

    CONSUMER:
        kafka-console-consumer.sh \

            --bootstrap-server my-release-kafka.kafka.svc.cluster.local:9092 \
            --topic test \
            --from-beginning
```

**Step 5:** Check updated information about your release using helm list command.

```execute
helm list -n kafka
```

Output:
```
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
my-release      kafka           2               2021-01-09 12:45:13.889656747 -0600 CST deployed        kafka-12.5.0    2.7.0
```

You have successfully upgraded your Kafka to the latest version of the Kafka chart.


# Rolling Back a Release

Each time you upgrade a release, a new revision of that release is created by Helm. A revision sets a fixed checkpoint to where you can come back if things don’t work as expected. 
If something goes wrong during the upgrade process, you can always rollback to a previous revision of a given Helm release with the helm rollback command.


If we want to undo the upgrade and rollback our Kafka release to its previous version, execute following command:

Execute rollback command :

```execute
helm rollback my-release 1 -n kafka
```

Output:

```output
Rollback was a success! Happy Helming!
```

This would rollback the Kafka installation to its previous release. 