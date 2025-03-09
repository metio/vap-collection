<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-host-ipc

Verifies that pods do not use the host IPC namespace.

Use the following query to list all pods in your cluster along with their current `hostIPC` usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(.spec | has("hostIPC")) | .metadata.namespace + "/" + .metadata.name'
```
