### Deploy following YAML file before running the deployment scripts for 21.0.x

1. Automation UI Configuration
```console apiVersion: core.automation.ibm.com/v1beta1
apiVersion: core.automation.ibm.com/v1beta1
kind: AutomationUIConfig
metadata:
  namespace: cnsi-baw-21-0-1
  name:  iaf-system
spec:
  description: automation-ui-config for CP4BA Cartridge
  license:
    accept: true
  version: 1.0.0
  tls: {}
  storage:
    class: cp4a-file-retain-gold-gid
```
2. Cartridge YAML
```console
apiVersion: core.automation.ibm.com/v1beta1
kind: Cartridge
metadata:
  namespace: cnsi-baw-21-0-1
  name: icp4ba
spec:
  description: cartridge for all CP4BA
  license:
    accept: true
  version: 1.0.0
 ```
 3. Patching scripts 01 : `DB2 pod (c-db2ucluster-cp4ba-db2u-0) is not ready`
 ```console
 oc patch $(oc get sts -lcomponent=db2oltp -oname -n=cnsi-baw-21-0-1) -n=cnsi-baw-21-0-1 -p='{"spec":{"template":{"spec":{"containers":[{"name":"db2u","tty":false}]}}}}}'
 ```
 4. Patching scripts 02 :
 ```console
 oc patch sts db2u-release-db2u -p='{"spec":{"template":{"spec":{"containers":[{"name":"db2u","tty":false}]}}}}}'
 ```
 5. Make changes on cluster_role.yaml and cluster_role_binding.yaml with cluster `<namespace>`
 6. [IBM Support for Limitation](https://www.ibm.com/support/pages/node/6426995/#v10-apic-support)
 7. [GitHub Support Limititation](https://github.ibm.com/dte-support/public/blob/master/CloudPaks/cp4ba-db2-install-issue-work-around.md)
