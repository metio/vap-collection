<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-privileged-containers

Verifies that pods do not run in privileged mode.

Use the following query to list all pods in your cluster along with their current privileged usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(.spec.containers[].securityContext.privileged == "true" or .spec.initContainers[].securityContext.privileged == "true" or .spec.ephemeralContainers[].securityContext.privileged == "true") | .metadata.namespace + "/" + .metadata.name'
```
