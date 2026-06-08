# Deployment

In the training, we will learn about Deployment.

> Navigate to the lab folder:

```bash
cd /workspaces/kubernetes-fundamentals/06_deployments
```

## Recreate rollout strategy

- Inspect deployment-v1.yaml definition file and create the deployment

  ```bash
  cat deployment-v1.yaml
  kubectl create -f deployment-v1.yaml

  # [TERMINAL-2] open a second terminal to watch pods
  watch -n 1 kubectl get pods

  # scale the number of replicas to 3 and take a look at the second terminal
  kubectl scale deployment my-deployment --replicas 3
  
  # change the image of the deployment and take a look at the second terminal
  kubectl set image deployment my-deployment nginx=nginx:1.19.3
  ```

## RollingUpdate rollout strategy

- Inspect and re-create the deployment

  > Pay attention to the deleted rollout strategy. Now Kubernetes defaults to the `rollingUpdate` rollout strategy.

  ```bash
  kubectl replace --force -f deployment-v2.yaml
  
  # change the image of the deployment and take a look at the second terminal
  kubectl set image deployment my-deployment nginx=nginx:1.19.3
  ```

- Take a look at the deployment and replicasets

  ```bash
  kubectl get deploy,rs
  ```

## Cleanup

Delete the Deployment

```bash
kubectl delete deployment my-deployment
```

Verify the deployment is deleted including all the associated pods and replicasets

```bash
kubectl get deploy,rs,po
```
