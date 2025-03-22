<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# require-seccomp-profile-type

Verifies that pods specify their seccomp profile type.

Use the following query to list all pods in your cluster along with their current seccomp profile type usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select([[.spec.securityContext.seccompProfile.type], .spec.containers[].securityContext.seccompProfile.type, .spec.initContainers[].securityContext.seccompProfile.type, .spec.ephemeralContainers[].securityContext.seccompProfile.type] | flatten | any_c(. != "RuntimeDefault" and . != "Localhost")) | .metadata.namespace + "/" + .metadata.name + ": " + ([[.spec.seccompProfile.type], .spec.containers[].securityContext.seccompProfile.type, .spec.initContainers[].securityContext.seccompProfile.type, .spec.ephemeralContainers[].securityContext.seccompProfile.type] | flatten | join(", "))'
```
