# Task : Kubernetes Persistent Storage + NodePort Service

## 🎯 Objective

The purpose of this task is to understand how Kubernetes provides persistent storage to an application and exposes that application through a NodePort Service.

In this lab, we create:

A PersistentVolume (PV)

A PersistentVolumeClaim (PVC)

An Apache HTTPD Pod

A NodePort Service

🏗️ Architecture

PersistentVolume (5Gi)
        │
        ▼
PersistentVolumeClaim (2Gi)
        │
        ▼
    Pod: pod-devops
        │
        ▼
  httpd:latest
        │
        ▼
Apache Document Root
/usr/local/apache2/htdocs
        │
        ▼
Service: web-devops
        │
        ▼
NodePort: 30008

## 1. Create the PersistentVolume

Create a file named pv.yaml:

apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-devops
spec:
  storageClassName: manual
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/data

Apply it:

kubectl apply -f pv.yaml

Verify:

kubectl get pv

Key concepts

5Gi — total storage capacity provided by the PV.

ReadWriteOnce (RWO) — the volume can be mounted as read-write by a single node.

manual — storage class used for the PV/PVC binding.

hostPath — uses a directory from the Kubernetes node.

## 2. Create the PersistentVolumeClaim

Create pvc.yaml:

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-devops
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi

Apply:

kubectl apply -f pvc.yaml

Verify:

kubectl get pvc

Expected status:

Bound

Check both PV and PVC:

kubectl get pv,pvc

PV vs PVC

PersistentVolume (PV) represents storage available to the cluster.

PersistentVolumeClaim (PVC) is a request for storage made by an application.

PV: 5Gi
     ↑
     │ Binding
     ↓
PVC: requests 2Gi

## 3. Create the Apache Pod

Apache HTTPD uses the following directory as its document root:

/usr/local/apache2/htdocs

Create pod.yaml:

apiVersion: v1
kind: Pod
metadata:
  name: pod-devops
  labels:
    app: pod-devops
spec:
  containers:
    - name: container-devops
      image: httpd:latest
      volumeMounts:
        - name: web-storage
          mountPath: /usr/local/apache2/htdocs
  volumes:
    - name: web-storage
      persistentVolumeClaim:
        claimName: pvc-devops

Apply:

kubectl apply -f pod.yaml

Verify:

kubectl get pods


## 4. Create the NodePort Service

Create service.yaml:

apiVersion: v1
kind: Service
metadata:
  name: web-devops
spec:
  type: NodePort
  selector:
    app: pod-devops
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008

Apply:

kubectl apply -f service.yaml

Verify:

kubectl get svc web-devops

Expected:

80:30008/TCP

## 5. Verify the Complete Setup

Check all resources:

kubectl get pv
kubectl get pvc
kubectl get pods
kubectl get svc

Check the Service endpoints:

kubectl get endpoints web-devops

 ## What I Learned

This lab helped me understand the complete relationship between Kubernetes storage, Pods, and Services.

Persistent Storage

The Pod does not directly create storage. Instead:

PV → PVC → Pod

The PVC requests storage from the available PV, and the Pod consumes that PVC.

Application Deployment

The Apache container runs using:

httpd:latest

The PVC is mounted at:

/usr/local/apache2/htdocs

This is Apache's document root.

Application Exposure

The NodePort Service provides external access:

NodePort: 30008

### The traffic flow is:

Client
  ↓
NodeIP:30008
  ↓
web-devops Service
  ↓
pod-devops:80
  ↓
Apache HTTPD