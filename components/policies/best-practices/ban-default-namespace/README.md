<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-default-namespace

Verifies that namespaced resources are not created/updated in the `default` namespace.

Use the following query to list all resources in the `default` namespace:

```shell
kubectl api-resources --verbs=list --namespaced --output name \
  | xargs -n 1 kubectl get --show-kind --ignore-not-found --namespace default
```
