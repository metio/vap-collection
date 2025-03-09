<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-host-network

Verifies that pods do not use the host network namespace.

Use the following query to list all pods in your cluster along with their current `hostNetwork` usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(.spec | has("hostNetwork")) | .metadata.namespace + "/" + .metadata.name'
```
