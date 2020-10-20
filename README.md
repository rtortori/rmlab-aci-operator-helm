# Helm repo for RMLAB ACI Operator
https://github.com/rtortori/rmlab-aci-operator

This is the Helm repo for the RMLAB Cisco ACI Kubernetes operator.

### Installation

Install Helm client and add the repo

```
helm repo add rmlab-aci-operator https://rtortori.github.io/rmlab-aci-operator-helm/
```

Install the operator

```
helm install aci-op rmlab-aci-operator/latest
```
