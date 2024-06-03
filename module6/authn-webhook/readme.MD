### Start authservice

```sh
make build
./bin/amd64/authn-webhook
```

### Create webhook config

```sh
mkdir -p /etc/config
cp webhook-config.json /etc/config
```

### Backup old apiserver

```sh
cp /etc/kubernetes/manifests/kube-apiserver.yaml ~/kube-apiserver.yaml
```

### Update apiserver configuration to enable webhook

```sh
cp specs/kube-apiserver.yaml /etc/kubernetes/manifests/kube-apiserver.yaml
```

### Create a personal access token in github and put your github personal access token to kubeconfig

```sh
vi ~/.kube/config
```

```yaml
- name: mfanjie
  user:
    token: <mytoken>
```

### Get pods by mfanjie

```sh
kubectl get po --user mfanjie
```

### Reset the env

```sh
cp ~/kube-apiserver.yaml /etc/kubernetes/manifests/kube-apiserver.yaml
```

#service account
```sh
kubectl create serviceaccount jenkins
kubectl apply -f jenkins-secret.yaml
kubect get secret -oyaml -n default
echo eyJhbGciOiJSUzI1NiIsImtpZCI6IkxYaDVRLXdobnpaOHNkN1gxV0JyQXRZMDcyTWtZSklMTjNZTTFPNEw1b3MifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6InRva2VuLXNlY3JldCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJqZW5raW5zIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiNmMyYzBiZWUtMjExOC00MzlkLThlY2EtMTY1YjYyN2IwNDdlIiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50OmRlZmF1bHQ6amVua2lucyJ9.Z2GTTWaDUsfIcqJvQ9EtvmZb8h9us8aXjiKgvAg8gaotRySyS3SKZZ2GnwgzUAaTc12ar3oySFGfwZ2E_irMY1tlJ8w7FEMvuYOUGUiYlyOBwoyVE4Cc04lh9M0X48J-sFivGdhBfYouOe1w5pTzMOTj65QFQkii_UR4wy0lfLvq2P8W_XtWlCDsD_dzSYYMCgILQBxgIYWTM-QZSzjkvN_gT7hWYO5Y1sjskqAyGFnW4p6WiuVGQsViZkVREnE8Dvxf8KxjsER-S89vx5i3601dlm-8ZfiLNpPM2cTdCSgBRdyuQVfCaNUspyh8GQhV6sDkcIAA6avAxiSwVATYTQ|base64 -d

curl https://10.161.1.87:6443/api/v1/namespaces/default -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IkxYaDVRLXdobnpaOHNkN1gxV0JyQXRZMDcyTWtZSklMTjNZTTFPNEw1b3MifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImplbmtpbnMtdG9rZW4tc2VjcmV0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImplbmtpbnMiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI2YzJjMGJlZS0yMTE4LTQzOWQtOGVjYS0xNjViNjI3YjA0N2UiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6ZGVmYXVsdDpqZW5raW5zIn0.E8RzAdrRM2lz99X88FFBJydexPbeehAQVAiP5SlEMDwRPDDDtG1EvLi4bfmc-VnMhKccWDH4Glydnrw3e3NF432F5h8cXO9ceufVYicd4YhvhvKJATycqGSmYRNYQyaLPLWdydKRqmV6oJ8sW-81JEs93BqqPC0pYKC7wYUzrQ47oxQjl4otug02UbDtYR6_VnerZjCtgz_A3vZ3hrkJfbJyHN15Q6jvq-9XV-eqJ_7ULoFaxNIK9H7uuNlA3h2mopzDN9UQxi1H9r8DQWOHqQyGY-U3z1zm_QU5-D1LL3x0NC6bRJ4kWm8uHGdO-ACHDblkYVQ3GxXZM5En6Js2Jg" -k
```
