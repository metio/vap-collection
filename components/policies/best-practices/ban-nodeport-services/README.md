<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-nodeport-services

Verifies that services do not use the type `NodePort`.

Use the following query to list all services in your cluster which are using type `NodePort`:

```shell
kubectl get services --all-namespaces --output yaml | yq '.items[] | select(.spec.type == "NodePort") | .metadata.namespace + "/" + .metadata.name'
```
