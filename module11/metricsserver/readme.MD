```sh
k get --raw "/api/v1/nodes/node1/proxy/metrics/resource"
```

```sh
apiVersion: apps/v1
kind: Deployment
spec:
    spec:
      containers:
      ...
      hostNetwork: true
      dnsPolicy: ClusterFirstWithHostNet
```
