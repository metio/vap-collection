# VAP Collection

This repository contains a collection of [ValidatingAdmissionPolicies](https://kubernetes.io/docs/reference/access-authn-authz/validating-admission-policy/) for Kubernetes >= 1.30.

These policies are based on [kyverno/policies](https://github.com/kyverno/policies) and were adjusted to work in environments that do not have a running Kyverno installation.

## Installation

All policies are managed with kustomize and can be installed by referencing overlays and/or components.

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

resources:
  # 'all' includes all existing policies
  - https://github.com/metio/vap-collection//overlays/all/?ref=<VERSION>
  # 'pod-security-standards-baseline' contains policies for https://kubernetes.io/docs/concepts/security/pod-security-standards/#baseline
  - https://github.com/metio/vap-collection//overlays/pod-security-standards-baseline/?ref=<VERSION>
  # 'pod-security-standards-restricted' contains policies for https://kubernetes.io/docs/concepts/security/pod-security-standards/#restricted
  - https://github.com/metio/vap-collection//overlays/pod-security-standards-restricted/?ref=<VERSION>
```
