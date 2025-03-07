<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# restrict-seccomp-profile-types

Verifies that pods can only use the following seccomp profile types:

- `RuntimeDefault`
- `Localhost`

Use the following query to list all pods in your cluster along with their current seccomp profile type usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select([[.spec.seccompProfile.type], .spec.containers[].securityContext.seccompProfile.type, .spec.initContainers[].securityContext.seccompProfile.type, .spec.ephemeralContainers[].securityContext.seccompProfile.type] | flatten | any_c(. != "RuntimeDefault" and . != "Localhost")) | .metadata.namespace + "/" + .metadata.name + ": " + ([[.spec.seccompProfile.type], .spec.containers[].securityContext.seccompProfile.type, .spec.initContainers[].securityContext.seccompProfile.type, .spec.ephemeralContainers[].securityContext.seccompProfile.type] | flatten | join(", "))'
```
