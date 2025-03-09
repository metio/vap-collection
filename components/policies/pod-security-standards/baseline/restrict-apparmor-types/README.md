<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# restrict-apparmor-types

Verifies that pods can only use the following AppArmor types:

- `RuntimeDefault`
- `Localhost`

Use the following query to list all pods in your cluster along with their current AppArmor type usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select([[.spec.securityContext.appArmorProfile.type], .spec.containers[].securityContext.appArmorProfile.type, .spec.initContainers[].securityContext.appArmorProfile.type, .spec.ephemeralContainers[].securityContext.appArmorProfile.type] | flatten | any_c(. != "RuntimeDefault" and . != "Localhost")) | .metadata.namespace + "/" + .metadata.name + ": " + ([[.spec.appArmorProfile.type], .spec.containers[].securityContext.appArmorProfile.type, .spec.initContainers[].securityContext.appArmorProfile.type, .spec.ephemeralContainers[].securityContext.appArmorProfile.type] | flatten | join(", "))'
```
