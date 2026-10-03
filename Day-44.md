# Task: Kubernetes Init Container with Shared emptyDir Volume

## Task Overview

Create a Kubernetes Deployment named ic-deploy-devops with one
replica. The Pod contains an Init Container and a Main Container that
share data through an emptyDir volume.

## Architecture Flow

Deployment → Pod → Init Container → Shared emptyDir Volume → Main
Container

## Step 1: Create the Deployment

The Deployment manages the Pod and ensures that the required Pod is
created and maintained.

Deployment name: ic-deploy-devops

Replicas: 1

Label: app: ic-devops

## Step 2: Configure the Init Container

The Init Container is named ic-msg-devops and uses the fedora:latest
image.

It runs:

/bin/bash -c 'echo Init Done - Welcome to xFusionCorp Industries > /ic/blog'

Its job is to create the /ic/blog file before the main container
starts.

## Step 3: Create the Shared Volume

An emptyDir volume named ic-volume-devops is created.

It is mounted at:

/ic

Both the Init Container and Main Container use the same volume, allowing
them to share the /ic/blog file.

Note: emptyDir storage exists for the lifetime of the Pod and is
removed when the Pod is deleted.

## Step 4: Configure the Main Container

The Main Container is named ic-main-devops and also uses the
fedora:latest image.

It continuously reads the file:

while true; do cat /ic/blog; sleep 5; done

This allows the Main Container to display the message created by the
Init Container.

## Step 5: Container Startup Sequence

Kubernetes follows this sequence:

Pod Created
    ↓
Init Container Starts
    ↓
Creates /ic/blog
    ↓
Init Container Completes Successfully
    ↓
Main Container Starts
    ↓
Main Container Reads /ic/blog

If the Init Container fails, the Main Container will not start.

Kubernetes YAML

apiVersion: apps/v1
kind: Deployment
metadata:
  name: ic-deploy-devops
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ic-devops
  template:
    metadata:
      labels:
        app: ic-devops
    spec:
      initContainers:
        - name: ic-msg-devops
          image: fedora:latest
          command:
            - /bin/bash
            - -c
            - echo Init Done - Welcome to xFusionCorp Industries > /ic/blog
          volumeMounts:
            - name: ic-volume-devops
              mountPath: /ic

      containers:
        - name: ic-main-devops
          image: fedora:latest
          command:
            - /bin/bash
            - -c
            - while true; do cat /ic/blog; sleep 5; done
          volumeMounts:
            - name: ic-volume-devops
              mountPath: /ic

      volumes:
        - name: ic-volume-devops
          emptyDir: {}

Useful Commands

Apply the Deployment

kubectl apply -f deployment.yml

Check the Pod

kubectl get pods

Check Init Container

kubectl logs <pod-name> -c ic-msg-devops

Expected output:

Init Done - Welcome to xFusionCorp Industries

Check Main Container

kubectl logs <pod-name> -c ic-main-devops