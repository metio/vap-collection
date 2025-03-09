<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-external-ip-services

Verifies that services of type `ExternalName` do not point to `localhost`.

Use the following query to list all services in your cluster which are using type `ExternalName` and point to `localhost`:

```shell
kubectl get services --all-namespaces --output yaml | yq '.items[] | select(.spec.type == "ExternalName" and .spec.externalName == "localhost") | .metadata.namespace + "/" + .metadata.name'
```
