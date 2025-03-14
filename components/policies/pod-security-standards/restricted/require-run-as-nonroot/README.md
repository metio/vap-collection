<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# require-run-as-nonroot

Verifies that pods do not allow privilege escalation.

Use the following query to list all pods in your cluster along with their current privilege escalation policy:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(((.spec.containers[].securityContext | has("runAsNonRoot") and .spec.containers[].securityContext.runAsNonRoot != "true") or (.spec.containers[].securityContext | has("runAsNonRoot") | not and .spec.securityContext.runAsNonRoot != "true")) or ((.spec.initContainers[].securityContext | has("runAsNonRoot") and .spec.initContainers[].securityContext.runAsNonRoot != "true") or (.spec.initContainers[].securityContext | has("runAsNonRoot") | not and .spec.securityContext.runAsNonRoot != "true")) or ((.spec.ephemeralContainers[].securityContext | has("runAsNonRoot") and .spec.ephemeralContainers[].securityContext.runAsNonRoot != "true") or (.spec.ephemeralContainers[].securityContext | has("runAsNonRoot") | not and .spec.securityContext.runAsNonRoot != "true"))) | .metadata.namespace + "/" + .metadata.name'
```
