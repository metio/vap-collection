<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-apparmor-annotation

Verifies that pods do not use the `container.apparmor.security.beta.kubernetes.io/*` annotation.

Use the following query to list all pods in your cluster along with their current annotation usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(.metadata.annotations[] | test("^container\.apparmor\.security\.beta\.kubernetes\.io/*$")) | .metadata.namespace + "/" + .metadata.name'
```
