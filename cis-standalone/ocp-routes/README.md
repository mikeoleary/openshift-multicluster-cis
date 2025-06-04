This example contains **working, tested** manifests that configure
- CIS in Multi-cluster mode (but only 1 cluster exists in my testing)
  - CIS is in standalone mode (there is only 1 CIS instance running, not multiple CIS instances across clusters)
  - there is a extended-spec-configmap
    - it defining 3 clusters under `externalClustersConfig`, however in testing only cluster1 actually existed, cluster2 and 3 did not exist.
    - it also defines additional settings for OCP routes under `extendedRouteSpec`
- A secure **OpenShift Route** resource
  - `--extended-spec-configmap` defines a ConfigMap which includes settings for Routes in given namespaces
- A demo app that can be run in OpenShift (eg doesn't bind to port 80)
  - demo app listens on 8443 (https) and 8080 (http)
  - in this demo, all traffic reaches app on 8443 (since reencrypt is in use)
- No ingress controller (NGINX, haproxy, etc) is used in this example.

This example uses OpenShift Routes. This example uses CIS 2.20.0, and the rbac and CRD definitions linked to in 2.20.0 [release notes](https://clouddocs.f5.com/containers/latest/reference/release-notes.html).