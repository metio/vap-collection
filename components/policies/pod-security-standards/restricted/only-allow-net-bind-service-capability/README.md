<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# only-allow-net-bind-service-capability

Verifies that pods can only add the `NET_BIND_SERVICE` capability.

Use the following query to list all pods in your cluster along with their current capability usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(.spec.containers[].securityContext.capabilities.add | length > 0 or .spec.initContainers[].securityContext.capabilities.add | length > 0 or .spec.ephemeralContainers[].securityContext.capabilities.add | length > 0) | .metadata.namespace + "/" + .metadata.name + ": " + ([.spec.containers[].securityContext.capabilities.add, .spec.initContainers[].securityContext.capabilities.add, .spec.ephemeralContainers[].securityContext.capabilities.add] | flatten | join(", "))'
```
