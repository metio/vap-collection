<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# restrict-selinux-types

Verifies that pods can only use the following SELinux types:

- `container_t`
- `container_init_t`
- `container_kvm_t`
- `container_engine_t`

Use the following query to list all pods in your cluster along with their current SELinux type usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select([[.spec.securityContext.seLinuxOptions.type], .spec.containers[].securityContext.seLinuxOptions.type, .spec.initContainers[].securityContext.seLinuxOptions.type, .spec.ephemeralContainers[].securityContext.seLinuxOptions.type] | flatten | any_c(. != "RuntimeDefault" and . != "Localhost")) | .metadata.namespace + "/" + .metadata.name + ": " + ([[.spec.seLinuxOptions.type], .spec.containers[].securityContext.seLinuxOptions.type, .spec.initContainers[].securityContext.seLinuxOptions.type, .spec.ephemeralContainers[].securityContext.seLinuxOptions.type] | flatten | join(", "))'
```
