# Ingress

In this training, we will set up an Ingress and expose an app showing a blue screen and an app showing a red screen.

> Navigate to the lab folder:

```bash
cd /workspaces/kubernetes-fundamentals/30_ingress
```

## Create the red application

```bash
kubectl create -f red.yaml
```

## Create the blue application

```bash
kubectl create -f blue.yaml
```

## Verify your steps

```bash
kubectl get pods,svc
```

## Inspect and create the resources for the ingress controller

```bash
# install NGINX ingress controller
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespace \
  --version 4.11.0

# verify everything is running
kubectl get deployments,pods,services -n ingress-nginx
```

## Inspect and create the ingress

```bash
kubectl create -f ingress.yaml
```

## Verify your ingress configuration

```bash
kubectl describe ing my-ingress
```

## Access the applications

```bash
# get the ip address of the ingress-controller loadbalancer
kubectl get svc ingress-nginx-controller -n ingress-nginx -o jsonpath='{.status.loadBalancer.ingress[].ip}'

# curl the red application
curl http://<EXTERNAL-IP>/red

# curl the blue application
curl http://<EXTERNAL-IP>/blue

# [TERMINAL-2] port-forward the ingress-controller loadbalancer
kubectl port-forward svc/ingress-nginx-controller -n ingress-nginx 8080:80

# get the url of the application red
echo "https://${CODESPACE_NAME}-8080.app.github.dev/red"

# get the url of the application blue
echo "https://${CODESPACE_NAME}-8080.app.github.dev/blue"
```

## Clean up

```bash
helm uninstall -n ingress-nginx ingress-nginx
kubectl delete -f .
```
