# Intro to kubernetes.
## 1. Install kubectl and minikube.
1. Follow the instruction in https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

2. Then setup minikube.
Run command `minikube start`
> Result:
✨  Automatically selected the docker driver. Other choices: qemu2, vmware, ssh
📌  Using Docker driver with root privileges
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image v0.0.46 ...
💾  Downloading Kubernetes v1.32.0 preload ...
    > preloaded-images-k8s-v18-v1...:  333.57 MiB / 333.57 MiB  100.00% 25.05 M
    > gcr.io/k8s-minikube/kicbase...:  500.31 MiB / 500.31 MiB  100.00% 11.98 M
🔥  Creating docker container (CPUs=2, Memory=7900MB) ...
🐳  Preparing Kubernetes v1.32.0 on Docker 27.4.1 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

## 2. Some basic kubernetes's commands 

1. `kubectl get nodes`
> Result:
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   17m   v1.32.0

It indicates that there is one node in the clust ther, it's role is master node.

2. `kubectl config get-contexts` to see which is the curren cluster we are working on.
> Result:
CURRENT   NAME       CLUSTER    AUTHINFO   NAMESPACE
*         minikube   minikube   minikube   default

3. `kubectl config use-contexts <cluster-name>` to choose the desired cluster.

## 3. Run a simple pod using command.
1. Create a pod.
Run the command `kubectl run nginx-pod --image=nginx`
> Result:
pod/nginx-pod created

2. List pods.
Run the command `kubectl get pods`
> Result:
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          2m37s

3. Get pod details.
Run the command `kubectl describe pod nginx-pod`
> Result:
Name:             nginx-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Fri, 07 Feb 2025 00:46:34 +0700
Labels:           run=nginx-pod
Annotations:      <none>
Status:           Running
IP:               10.244.0.3
IPs:
  IP:  10.244.0.3
Containers:
  nginx-pod:
    Container ID:   docker://4e0359a1c59376e5d64a10310c84cdbfb9149dfdbc5077852142386c416387f3
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:91734281c0ebfc6f1aea979cffeed5079cfe786228a71cc6f1f46a228cde6e34
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Fri, 07 Feb 2025 00:46:41 +0700
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-w2ffk (ro)
...

4. Delete the pod.
Run the command `kubectl delete pod nginx-pod`
> Result:
pod "nginx-pod" deleted

## Run a simple pod using yaml file

1. Write a config file named nginx-pod.yaml .
2. Run command `kubectl apply -f nginx-pod.yaml`.
> Result:
pod/nginx-pod created

3. Check list of pods by running `kubectl get pods -o wide`
> Result:
NAME        READY   STATUS    RESTARTS   AGE   IP           NODE       NOMINATED NODE   READINESS GATES
nginx-pod   1/1     Running   0          79s   10.244.0.4   minikube   <none>           <none>


4. Delete pod by running `kubectl delete -f nginx-pod.yaml` .
> Result:
pod "nginx-pod" deleted

> Check the list of pods:
No resources found in default namespace.

