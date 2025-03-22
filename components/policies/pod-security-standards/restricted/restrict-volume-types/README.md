<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# restrict-volume-types

Verifies that pods only specify volumes using the following types:

- `configMap`
- `csi`
- `downwardAPI`
- `emptyDir`
- `ephemeral`
- `persistentVolumeClaim`
- `projected`
- `secret`

Use the following query to list all pods in your cluster along with their current volume type usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(.spec.volumes[] | (has("configMap") | not and has("csi") | not and has("downwardAPI") | not and has("emptyDir") | not and has("ephemeral") | not and has("persistentVolumeClaim") | not and has("projected") | not and has("secret") | not)) | .metadata.namespace + "/" + .metadata.name'
```
