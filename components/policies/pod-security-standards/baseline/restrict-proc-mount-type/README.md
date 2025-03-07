<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# restrict-proc-mount-type

Verifies that pods can only use the following `/proc` mount types:

- `Default`

Use the following query to list all pods in your cluster along with their current `/proc` mount usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select([.spec.containers[].securityContext.procMount, .spec.initContainers[].securityContext.procMount, .spec.ephemeralContainers[].securityContext.procMount] | flatten | any_c(. != "Default")) | .metadata.namespace + "/" + .metadata.name + ": " + ([.spec.containers[].securityContext.procMount, .spec.initContainers[].securityContext.procMount, .spec.ephemeralContainers[].securityContext.procMount] | flatten | join(", "))'
```
