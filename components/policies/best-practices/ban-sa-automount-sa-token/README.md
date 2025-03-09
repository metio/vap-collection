<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-sa-automount-sa-token

Verifies that service accounts do not automatically mount their service account token.

Use the following query to list all service accounts in your cluster which are automounting their token:

```shell
kubectl get serviceaccounts --all-namespaces --output yaml | yq '.items[] | select(.automountServiceAccountToken != "false") | .metadata.namespace + "/" + .metadata.name'
```
