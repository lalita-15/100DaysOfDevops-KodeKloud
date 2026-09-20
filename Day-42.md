# Kubernetes Sidecar Pattern | Nginx Logging with Shared emptyDir Volume

## Task

### Create a Pod named webserver with two containers:

nginx-container using nginx:latest

sidecar-container using ubuntu:latest

Create an emptyDir volume named shared-logs

Mount the volume at /var/log/nginx in both containers

The sidecar should read Nginx access and error logs every 30 seconds

Keep the containers in a running state

## Problem

The second container is specified as an init container. Normally, an
init container completes its work and exits.

But this task requires the containers to remain in the Running
state. Therefore, the sidecar needs to continue running instead of
exiting.

## Solution

Use a native Kubernetes sidecar by adding:

## restartPolicy: Always

to the sidecar container.

## Pod Configuration

apiVersion: v1
kind: Pod
metadata:
  name: webserver
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx

  initContainers:
    - name: sidecar-container
      image: ubuntu:latest
      restartPolicy: Always
      command:
        - sh
        - -c
        - while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx

  volumes:
    - name: shared-logs
      emptyDir: {}

### How It Works

Nginx Container
      |
      | Generates logs
      v
shared-logs (emptyDir)
      |
      | Shared log files
      v
Sidecar Container
      |
      | Reads logs every 30 seconds
      v
Log Aggregation

## Commands

kubectl apply -f webserver.yaml
kubectl get pod webserver
kubectl describe pod webserver
kubectl logs webserver -c sidecar-container

