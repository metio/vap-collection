<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# restrict-sysctls

Verifies that pods can only use the following sysctls:

- `kernel.shm_rmid_forced`
- `net.ipv4.ip_local_port_range`
- `net.ipv4.ip_unprivileged_port_start`
- `net.ipv4.tcp_syncookies`
- `net.ipv4.ping_group_range`
- `net.ipv4.ip_local_reserved_ports`
- `net.ipv4.tcp_keepalive_time`
- `net.ipv4.tcp_fin_timeout`
- `net.ipv4.tcp_keepalive_intvl`
- `net.ipv4.tcp_keepalive_probes`

Use the following query to list all pods in your cluster along with their current sysctls usage:

```shell
kubectl get pods --all-namespaces --output go-template --template='{{- range .items -}}
{{- if and .spec.securityContext .spec.securityContext.sysctls -}}
{{- if gt (len .spec.securityContext.sysctls) 0 }}
{{ .metadata.namespace }}/{{ .metadata.name }}: {{ range $index, $sysctl := .spec.securityContext.sysctls }}{{ if $index }}, {{ end }}{{ $sysctl.name }}{{ end }}
{{- end -}}
{{- end -}}
{{- end -}}'
```
