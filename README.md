Generate CA
```
openssl req -x509 -nodes -newkey rsa:2048 -keyout ca.key -days 1826 -out ca.crt -subj '/CN=root-ca'
# replace oc with kubectl if necessary
oc create secret generic ca-secret --from-file=./ca.key --from-file=./ca.crt
```
Create single node cluster with RAY_USE_TLS = "1"
```bash
oc apply -f https://raw.githubusercontent.com/tedhtchang/kuberay-tls/master/ray-cluster.mini.yaml
```

Clean up
```bash
oc delete -f https://raw.githubusercontent.com/tedhtchang/kuberay-tls/master/ray-cluster.mini.yaml
oc delete secret ca-secret
```
