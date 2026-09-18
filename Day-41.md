# Kubernetes Shared Volume Using `emptyDir`

## 📌 Task Overview

The objective of this task is to create a Kubernetes Pod with **two containers** that share temporary storage using an `emptyDir` volume.

Data created by the first container should be accessible from the second container through the same shared volume.

---

## 🎯 Requirements

* Create a Pod named `volume-share-datacenter`
* Create two containers inside the Pod
* Use `ubuntu:latest` image for both containers
* Container 1:

  * Name: `volume-container-datacenter-1`
  * Mount path: `/tmp/blog`
* Container 2:

  * Name: `volume-container-datacenter-2`
  * Mount path: `/tmp/games`
* Create an `emptyDir` volume named `volume-share`
* Run a `sleep` command so both containers remain running
* Create `blog.txt` inside the first container
* Verify that the same file is available inside the second container

---

## 🏗️ Architecture

```text
                 Kubernetes Pod
          volume-share-datacenter
                     |
          +----------+----------+
          |                     |
          ▼                     ▼
 Container 1               Container 2
 volume-container-         volume-container-
 datacenter-1              datacenter-2
          |                     |
    /tmp/blog              /tmp/games
          |                     |
          +----------+----------+
                     |
                     ▼
              volume-share
                emptyDir
                     |
                     ▼
                blog.txt
```

---

## 1. Create YAML File

```bash
vi volume-share-datacenter.yaml
```

Add the following configuration:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-share-datacenter
spec:
  containers:
    - name: volume-container-datacenter-1
      image: ubuntu:latest
      command: ["sleep", "3600"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/blog

    - name: volume-container-datacenter-2
      image: ubuntu:latest
      command: ["sleep", "3600"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/games

  volumes:
    - name: volume-share
      emptyDir: {}
```

---

## 2. Create the Pod

```bash
kubectl apply -f volume-share-datacenter.yaml
```

Check the Pod:

```bash
kubectl get pod volume-share-datacenter
```

Expected output:

```text
NAME                       READY   STATUS    RESTARTS   AGE
volume-share-datacenter    2/2     Running   0          ...
```

The `2/2` indicates that both containers are running successfully.

---

## 3. Exec into the First Container

Access the first container:

```bash
kubectl exec -it volume-share-datacenter \
  -c volume-container-datacenter-1 -- /bin/bash
```

Create the required file:

```bash
echo "Welcome to xFusionCorp Industries" > /tmp/blog/blog.txt
```

Verify the file:

```bash
cat /tmp/blog/blog.txt
```

Expected output:

```text
Welcome to xFusionCorp Industries
```

Exit the container:

```bash
exit
```

---

## 4. Verify the Shared File in the Second Container

Access the second container:

```bash
kubectl exec -it volume-share-datacenter \
  -c volume-container-datacenter-2 -- /bin/bash
```

Check the mounted directory:

```bash
ls -l /tmp/games
```

Expected:

```text
blog.txt
```

Read the file:

```bash
cat /tmp/games/blog.txt
```

Expected output:

```text
Welcome to xFusionCorp Industries
```

---

## 5. Quick Verification Commands

Verify from the first container:

```bash
kubectl exec volume-share-datacenter \
  -c volume-container-datacenter-1 -- \
  cat /tmp/blog/blog.txt
```

Verify from the second container:

```bash
kubectl exec volume-share-datacenter \
  -c volume-container-datacenter-2 -- \
  cat /tmp/games/blog.txt
```

Both should return:

```text
Welcome to xFusionCorp Industries
```

---

## 🔑 Key Concept: `emptyDir`

`emptyDir` is a temporary Kubernetes volume that is created when a Pod is assigned to a node.

Multiple containers within the **same Pod** can mount the same `emptyDir` volume and share data through it.

In this task:

```text
Container 1
/tmp/blog
     |
     ▼
volume-share
(emptyDir)
     ▲
     |
/tmp/games
Container 2
```

Although the containers use different mount paths, both paths point to the same underlying `volume-share`.

Therefore:

```text
/tmp/blog/blog.txt
```

in Container 1 is the same shared file as:

```text
/tmp/games/blog.txt
```

in Container 2.

---

## 🧠 What I Learned

* How to create a multi-container Kubernetes Pod
* How to define an `emptyDir` volume
* How to mount one volume into multiple containers
* How to use `kubectl exec` with a specific container
* How containers within the same Pod can share temporary data
* How different mount paths can reference the same underlying volume

---

## 🛠️ Technologies Used

* Kubernetes
* Ubuntu
* YAML
* kubectl
* Containers
* `emptyDir` Volume

---

