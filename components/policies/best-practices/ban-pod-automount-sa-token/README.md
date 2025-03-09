<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-pod-automount-sa-token

Verifies that pods do not automatically mount their service account token.

Use the following query to list all pods in your cluster which are automounting their service account token:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(.spec.automountServiceAccountToken != "false") | .metadata.namespace + "/" + .metadata.name'
```
