---
title: How to Deploy Test Client for Kafka
description: This tutorial explains how to deploy a test client that will execute scripts against the Kafka cluster
---


### Deploy Test Client for Kafka

Now you are going to deploy a test client that will execute scripts against the Kafka cluster.

Execute the below command to create `testclient.yaml` :

```execute
cat <<'EOF' > testclient.yaml
apiVersion: v1
kind: Pod
metadata:
  name: testclient
spec:
  containers:
  - name: kafka
    image: solsson/kafka:0.11.0.0
    command:
      - sh
      - -c
      - "exec tail -f /dev/null"
EOF
```

Execute the command to create the client:

```execute
kubectl -n kafka apply -f testclient.yaml
```

Now check the `testclient` pod up and running by executing the below command:

```execute
kubectl get pods -n kafka
```

Output:

```output
NAME                     READY   STATUS    RESTARTS   AGE
my-release-kafka-0       1/1     Running   0          65m
my-release-zookeeper-0   1/1     Running   0          65m
testclient               1/1     Running   0          56m
```

Now using the `testclient`, you will create the first `topic`  “messages”, with one partition and replication factor ‘1’, which you are going to use to post messages:

```execute
kubectl -n kafka exec -it testclient -- ./bin/kafka-topics.sh --zookeeper my-release-zookeeper:2181 --topic messages --create --partitions 1 --replication-factor 1
```

Output:

```output
Created topic "messages".
```

Here you need to use the correct hostname for zookeeper cluster and the topic configuration.

Now to send and receive the messages you will need to have two terminals. Let's get that using our`Developer Dashboard` tab. 

### Get Multiple Terminals

**Step 1 :**Click on the `Developer Dashboard` tab on top.

![](_images/developer-dashboard.png)

It will open a Visual Studio Code Editor.

**Step 2 :** Click on Menu --> View --> Terminal

![](_images/terminal.png)



**Step 3 :** Click on the `+` button at right top corner of your terminal to get another terminal.

 ![](_images/add-terminal.png)

**Step 4 :** Choose `code-server` as the terminal option.

![](_images/code-server.png)



**Step 5 :** Now you will have two terminals where you can switch.

![](_images/terminal-switch.png)

### Send and Receive Messages

**NOTE :**  Copy and execute below command in both terminals for disabling network logs on Kubernetes when running `kubectl exec` commands.

```
unset DEBUG
```
Follow the below steps in parallel terminals.
**Terminal 1:**

Now copy and execute the below command to create a producer that will publish messages to the topic.

```
kubectl -n kafka exec -ti testclient -- ./bin/kafka-console-producer.sh --broker-list my-release-kafka:9092 --topic messages
```

You can try sending some messages like below:

![](_images/sender.png)

Execute below command to exit :

```
exit
```

**Terminal 2:**

In a separate terminal,copy and execute the below command to open a consumer session so that you can see the messages as you send it.

```
kubectl -n kafka exec -ti testclient -- ./bin/kafka-console-consumer.sh --bootstrap-server my-release-kafka:9092 --topic messages
```

You will get the messages sent :

![](_images/receiver.png)

Execute below command to exit :

```
exit
```

Here you Go !! Your Kafka cluster is working correctly.
