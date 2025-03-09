<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# ban-host-process

Verifies that pods do not run Windows HostProcess containers.

Use the following query to list all pods in your cluster along with their current host process usage:

```shell
kubectl get pods --all-namespaces --output yaml | yq '.items[] | select(.spec.containers[].securityContext.windowsOptions.hostProcess == "true" or .spec.initContainers[].securityContext.windowsOptions.hostProcess == "true" or .spec.ephemeralContainers[].securityContext.windowsOptions.hostProcess == "true") | .metadata.namespace + "/" + .metadata.name'
```
