<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# require-disabled-privilege-escalation

Verifies that pods do not allow privilege escalation.

Use the following query to list all pods in your cluster along with their current privilege escalation policy:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(.spec.containers[].securityContext.allowPrivilegeEscalation == "true" or .spec.initContainers[].securityContext.allowPrivilegeEscalation == "true" or .spec.ephemeralContainers[].securityContext.allowPrivilegeEscalation == "true") | .metadata.namespace + "/" + .metadata.name'
```
