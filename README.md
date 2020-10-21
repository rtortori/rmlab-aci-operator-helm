# Helm repo for RMLAB ACI Operator

##### This is the Helm repo for the RMLAB Cisco ACI Kubernetes operator.<br>
You can find the code [here](https://github.com/rtortori/rmlab-aci-operator) 

### Installation

Install Helm client and add the repo

```
helm repo add rmlab-aci-operator https://rtortori.github.io/rmlab-aci-operator-helm/
```

#### Install the operator

Kubernetes install:

```
helm install aci-op rmlab-aci-operator/latest
```

Openshift install

```
helm install aci-op rmlab-aci-operator/latest --set global.containerPlatform=openshift
```

### Customization

The operator gives the option to customize the installation and alter the behavior.<br>

To list the default values

```
helm show values rmlab-aci-operator/latest
```

The following table describes each option

| Key                                                        | Description                                                                                                                                                                                                                                                                                        |
|------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| global.containerPlatform                                   | The container platform you are using. Specifying 'openshift', each CR will create by default a project instead of a namespace (you can still override in the CR creation). Also, the controller will deploy in the 'aci-containers-system' namespace. Any other value will default to 'kubernetes' |
| global.kubeCreateResource                                  | COSMETIC. What the CR will create when running on Kubernetes. This is just used in the post install notification and will not affect the operator behavior                                                                                                                                         |
| global.openshiftCreateResource                             | COSMETIC. What the CR will create when running on Openshift. This is just used in the post install notification and will not affect the operator behavior                                                                                                                                          |
| aciCNI.kubeNamespace                                       | The namespace used by the ACI CNI in Kubernetes. Defaults to 'kube-system'                                                                                                                                                                                                                         |
| aciCNI.openshiftNamespace                                  | The namespace used by the ACI CNI in Openshift. Defaults to 'aci-containers-system'                                                                                                                                                                                                                |
| aciCNI.configMaps.aciContainersConfigMap                   | The ACI CNI configMap name. Defaults to 'aci-containers-config'                                                                                                                                                                                                                                    |
| aciCNI.secrets.aciUserCertSecret                           | The ACI CNI Cert secret name. Defaults to 'aci-user-cert'                                                                                                                                                                                                                                          |
| controller.replicaCount                                    | How many pods the controller will spin up                                                                                                                                                                                                                                                          |
| controller.labels.name                                     | The 'name' label in the controller deployment                                                                                                                                                                                                                                                      |
| controller.image.repository                                | The image for the controller (with no tags)                                                                                                                                                                                                                                                        |
| controller.image.pullPolicy                                | The pull policy for the controller image                                                                                                                                                                                                                                                           |
| controller.image.tag                                       | The tag for the controller image                                                                                                                                                                                                                                                                   |
| crd.names.shortName                                        | A short name to call AciNamespace. It defaults to 'aci'. In this case you can issue 'kubectl get aci' to fetch the AciNamespaces configured                                                                                                                                                        |
| crd.additionalPrinterColumns.epgContractMasterDef          | COSMETIC. The EPG Master contract column name for the 'kubectl get acinamespaces' command output                                                                                                                                                                                                   |
| crd.additionalPrinterColumns.bridgeDomainDef               | COSMETIC. The ACI Bridge Domain column name for the 'kubectl get acinamespaces' command output                                                                                                                                                                                                     |
| crd.additionalPrinterColumns.masterEPGConsumerContractsDef | COSMETIC. The consumer contracts for master EPG column name for the 'kubectl get acinamespaces' command output                                                                                                                                                                                     |
| crd.additionalPrinterColumns.masterEPGProviderContractsDef | COSMETIC. The provider contracts for master EPG column name for the 'kubectl get acinamespaces' command output                                                                                                                                                                                     |
| crd.additionalPrinterColumns.aciNsEPGConsumerContractsDef  | COSMETIC. The consumer contracts column name for the 'kubectl get acinamespaces' command output                                                                                                                                                                                                    |
| crd.additionalPrinterColumns.aciNsEPGProviderContractsDef  | COSMETIC. The provider contracts column name for the 'kubectl get acinamespaces' command output                                                                                                                                                                                                    |
| crd.additionalPrinterColumns.operatorManaged               | COSMETIC. The column name that describes if the operator is managing resources or not, for the 'kubectl get acinamespaces' command output                                                                                                                                                          |
| crd.specs.aciDefaultApplicationProfileName                 | The default ACI Application Profile (you can still override in the CR definition)                                                                                                                                                                                                                  |
| crd.specs.aciDefaultBridgeDomainName                       | The default ACI Bridge Domain (you can still override in the CR definition)                                                                                                                                                                                                                        |
| crd.cleanupImage                                           | When you uninstall the operator, a job will cleanup the AciNamespaces before removing the rest. This is the image used by this job                                                                                                                                                                 |
| serviceAccount.name                                        | The operator creates a dedicated serviceaccount for the controller, this is the name of the serviceaccount                                                                                                                                                                                         |


