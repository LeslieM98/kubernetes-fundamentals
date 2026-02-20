# Node Selector

In this training course, we will learn about Node Selector.

> Navigate to the lab folder:

```bash
cd /workspaces/kubernetes-fundamentals/21_scheduling-node-selector
```

## Show all Nodes with its Labels

```bash
kubectl get nodes --show-labels
```

## Add a Label to a node

```bash
kubectl label node my-cluster-worker preferred=true
```

## Inspect deployment.yaml definition file and create the deployment

```bash
cat deployment.yaml
kubectl create -f deployment.yaml
```

## Verify that all the pods of the deployment are running on the labeled node

```bash
kubectl get pods -o wide
```

## Cleanup

```bash
kubectl label node my-cluster-worker preferred-
kubectl delete deployment my-deployment
```
