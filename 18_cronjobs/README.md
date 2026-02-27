# CronJob

In this training course, we will create a job which will run every minute.

> Navigate to the lab folder:

```bash
cd /workspaces/kubernetes-fundamentals/18_cronjobs
```

## Inspect cronjob.yaml definition file and create the cronjob

```bash
cat cronjob.yaml
kubectl create -f cronjob.yaml

# [TERMINAL-2] watch the running jobs and the pods
watch -n 1 kubectl get pods,jobs

# recreate the cronjob
kubectl create -f cronjob.yaml
```

> It can take a while that the job is completed.

## Cleanup

```bash
kubectl delete cronjobs --all
```
