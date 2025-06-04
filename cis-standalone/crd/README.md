This example contains **working, tested** manifests that configure
- CIS in Multi-cluster mode (but only 1 cluster exists in my testing)
  - CIS is in standalone mode (there is only 1 CIS instance running, not multiple CIS instances across clusters)
  - there is a extended-spec-configmap defining 3 clusters, however in testing only cluster1 actually existed, cluster2 and 3 did not exist.
  - The VirtualServer (VS) custom resource (CR) must specify the "multiClusterServices" configuration under the pool setting
- A secure https VS CR
  - tlsProfile is also included, termination type is `reencrypt`
  - httpTraffic is set to `redirect`, so a port 80 VIP is created for redirect to port 443
- A demo app that can be run in OpenShift (eg doesn't bind to port 80)
  - demo app listens on 8443 (https) and 8080 (http)
  - in this demo, all traffic reaches app on 8443 (since reencrypt is in use)
- No ingress controller (NGINX, haproxy, etc) is used in this example.

This example does not use OpenShift Routes. This example uses CIS 2.20.0, and the rbac and CRD definitions linked to in 2.20.0 [release notes](https://clouddocs.f5.com/containers/latest/reference/release-notes.html).