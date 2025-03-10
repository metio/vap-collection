<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# require-requests-limits

Verifies that pods define requests for CPU and memory as well as memory limits.

Use the following query to list all pods in your cluster along with their current resource usage:

```shell
kubectl get pods --all-namespaces --output custom-columns='NAMESPACE:.metadata.namespace, NAME:.metadata.name, CPU_REQUEST:.spec.containers[*].resources.requests.cpu, MEMORY_REQUEST:.spec.containers[*].resources.requests.memory, MEMORY_LIMIT:.spec.containers[*].resources.limits.memory'
```
