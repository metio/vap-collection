<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-selinux-user

Verifies that pods do not set a SELinux user.

Use the following query to list all pods in your cluster along with their current SELinux user usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select([[.spec.securityContext.seLinuxOptions.user], .spec.containers[].securityContext.seLinuxOptions.user, .spec.initContainers[].securityContext.seLinuxOptions.user, .spec.ephemeralContainers[].securityContext.seLinuxOptions.user] | flatten | any_c(. != "")) | .metadata.namespace + "/" + .metadata.name + ": " + ([[.spec.seLinuxOptions.user], .spec.containers[].securityContext.seLinuxOptions.user, .spec.initContainers[].securityContext.seLinuxOptions.user, .spec.ephemeralContainers[].securityContext.seLinuxOptions.user] | flatten | join(", "))'
```
