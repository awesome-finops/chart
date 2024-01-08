```
helm repo add apepipe-expire https://awesome-finops.github.io/chart
helm repo update apepipe-expire
helm install apepipe-expire apepipe-expire/apepipe-expire -f apepipe-expire-values.yaml --namespace apepipe-expire --create-namespace
```
apepipe-expire-values.yaml (You can add more resources type to expire)
```
env:
  - name: RESOURCES
    value: v1;Pod,apps/v1;Deployment,v1;Secret
```

add annotations with "apepipe/expire", the resource will be deleted when the set duration reached after its creation.

you can test by below pod:
k apply -f my-pod.yaml
```
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  annotations:
    apepipe/expire: 30s
spec:
  containers:
    - name: alpine
      image: alpine
      command:
        - sleep
        - infinity
```



