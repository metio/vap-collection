<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-host-pid-usage

Verifies that pods do not use the host process ID namespace.

Use the following query to list all pods in your cluster along with their current `hostPID` usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(.spec | has("hostPID")) | .metadata.namespace + "/" + .metadata.name'
```
