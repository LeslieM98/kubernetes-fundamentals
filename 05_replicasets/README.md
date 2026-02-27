# ReplicaSet

In this training, we will learn about Replicasets.

> Navigate to the lab folder:

```bash
cd /workspaces/kubernetes-fundamentals/05_replicasets
```

## Inspect the replicaset.yaml definition file and create the replicaset

```bash
cat replicaset.yaml
kubectl create -f replicaset.yaml
```

> Find and fix the two issues in there. Note, that you haven't finished this section until the pod of the ReplicaSet is in Running state.

## Take a look at the number of Pods

```bash
kubectl get pods
```

## Scale the number of replicas to 3

```bash
# [TERMINAL-2] open a second terminal to watch pods
watch -n 1 kubectl get pods

# scale the replicaset
kubectl scale replicaset my-replicaset --replicas 3
```

## Delete one of the Pods

```bash
# [TERMINAL-2] open a second terminal to watch pods
watch -n 1 kubectl get pods

# delete one pod
kubectl delete pod <POD-NAME>
```

> Note that the pod gets recreated due to we claimed for 3 running pods in the replicaset.

## Cleanup

Delete the ReplicaSet

```bash
kubectl delete replicaset my-replicaset
```

Verify if replicaset is delete including all the associated pods

```bash
kubectl get rs,po
```
