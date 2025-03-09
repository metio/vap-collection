<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-selinux-role

Verifies that pods do not set a SELinux role.

Use the following query to list all pods in your cluster along with their current SELinux role usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select([[.spec.securityContext.seLinuxOptions.role], .spec.containers[].securityContext.seLinuxOptions.role, .spec.initContainers[].securityContext.seLinuxOptions.role, .spec.ephemeralContainers[].securityContext.seLinuxOptions.role] | flatten | any_c(. != "")) | .metadata.namespace + "/" + .metadata.name + ": " + ([[.spec.seLinuxOptions.role], .spec.containers[].securityContext.seLinuxOptions.role, .spec.initContainers[].securityContext.seLinuxOptions.role, .spec.ephemeralContainers[].securityContext.seLinuxOptions.role] | flatten | join(", "))'
```
