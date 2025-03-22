<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# require-run-as-non-root-user

Verifies that pods do not run as root user.

Use the following query to list all pods in your cluster along with their current user:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(.spec.containers[].securityContext.runAsUser == 0 or .spec.initContainers[].securityContext.runAsUser == 0 or .spec.ephemeralContainers[].securityContext.runAsUser == 0 or .spec.securityContext.runAsUser == 0) | .metadata.namespace + "/" + .metadata.name'
```
