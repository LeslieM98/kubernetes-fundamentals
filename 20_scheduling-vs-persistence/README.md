# Scheduling versus Persistence

In this lab you will learn about the side effects of persistence onto scheduling.

> Navigate to the lab folder:

```bash
cd /workspaces/kubernetes-fundamentals/20_scheduling-vs-persistence
```

## Non-persisting Deployments

```bash
# create the deployment
kubectl create -f non-persisting-deployment.yaml

# show the pods including the worker node info
kubectl get pods -o wide
```

> Note that the pods are spread across all worker nodes for High Availability. This is the default behaviour of the Kubernetes Scheduler.

## Persisting Deployments

```bash
# create the deployment
kubectl create -f persisting-deployment.yaml

# show the pods including the worker node info
kubectl get pods -o wide
```

> Note that the persisting pods got scheduled on one worker node due to they claim for a directory existing on one of the worker nodes.

> Note changing the accessmode to `ReadOnlyMany` in the PVC will also have no effect on the behaviour of the Scheduler. It is still storage provided by `localpath` and not via network attached storage.

## Cleanup

```bash
kubectl delete deployment --all
```
