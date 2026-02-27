# Job

In this training, we will create a job and parallelize its execution.

> Navigate to the lab folder:

```bash
cd /workspaces/kubernetes-fundamentals/17_jobs
```

## Inspect job.yaml definition file and create the job

```bash
cat job.yaml
kubectl create -f job.yaml
```

## Take a look at running Jobs and the Pods

> It can take a while that the job is completed.

```bash
kubectl get pods,jobs
```

## Increase the amount of executions to 10 and parallelize them

```yaml
spec:
  completions: 10
  parallelism: 5
  template:
```

```bash
# [TERMINAL-2] watch the running jobs and the pods
watch -n 1 kubectl get pods,jobs

# recreate the job
kubectl replace -f job.yaml  --force
```

## Clean up

```bash
kubectl delete jobs --all
```
