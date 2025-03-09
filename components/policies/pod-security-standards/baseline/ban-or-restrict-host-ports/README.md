<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-or-restrict-host-ports

Verifies that pods do not use host ports or their usage is limited to a known list of allowed ports.

Use the following query to list all pods in your cluster along with their current host port usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(.spec.containers[].ports[].hostPort > 0 or .spec.initContainers[].ports[].hostPort > 0 or .spec.ephemeralContainers[].ports[].hostPort > 0) | .metadata.namespace + "/" + .metadata.name + ": " + ([.spec.containers[].ports[].hostPort, .spec.initContainers[].ports[].hostPort, .spec.ephemeralContainers[].ports[].hostPort] | flatten | join(", "))'
```
