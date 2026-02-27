# StatefulSets

In the training, we will learn about Statefulsets.

> Navigate to the lab folder:

```bash
cd /workspaces/kubernetes-fundamentals/14_statefulsets
```

## Scaling

### Create service and statefulset

- Inspect service.yaml definition file and create the service

  ```bash
  cat service.yaml
  kubectl create -f service.yaml
  ```

- Inspect and create the sts

  ```bash
  # [TERMINAL-2] open a second terminal to watch pods
  watch -n 1 kubectl get sts,pv,pvc,pods

  # create the statefulset
  kubectl create -f sts.yaml
  ```

  > Take note that the replicas are created one by one and not all at the same time.

- Print the content of the state file of the last built pod

  ```bash
  kubectl exec -it my-sts-2 -- cat /app/state
  ```

### Scale down the statefulset

  ```bash
  # [TERMINAL-2] open a second terminal to watch pods
  watch -n 1 kubectl get sts,pv,pvc,pods

  # trigger scaling down the statefulset
  kubectl scale sts my-sts --replicas 2
  ```

  > Note that the pv and the pvc will not get deleted.

### Scale up the statefulset

- Scale up the statefulset

  ```bash
  kubectl scale sts my-sts --replicas 3
  ```

- Printout the content of the state file of the last built pod

  > Take note that the same pv and pvc got bound to the pod but the IP of the pod has changed.

  ```bash
  kubectl exec -it my-sts-2 -- cat /app/state
  ```

## Headless Service

### Get IPs of all pods of the statefulset

```bash
kubectl run -it nslookup --image nicolaka/netshoot --restart=Never --rm -- nslookup my-service
```

> This should give you a list of ip addresses of all the Pods within the StatefulSet. You can verify the correctness of those via `kubectl get pods -o wide`

## Clean up

```bash
kubectl delete svc,sts,pvc,pv --all
```
