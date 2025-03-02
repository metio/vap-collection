<!--
SPDX-FileCopyrightText: The vap-collection Authors
SPDX-License-Identifier: Apache-2.0
 -->

# VAP Collection

This repository contains a collection of [ValidatingAdmissionPolicies](https://kubernetes.io/docs/reference/access-authn-authz/validating-admission-policy/) for Kubernetes >= 1.30.

These policies are based on [kyverno/policies](https://github.com/kyverno/policies) and were adjusted to work in environments that do not have a running Kyverno installation.

## Installation

All policies are managed with kustomize and can be installed by referencing overlays and/or components. Check the [releases page](https://github.com/metio/vap-collection/releases) for available versions.

### Overlays

The following overlays are available in this repository. Feel free to enable as many of them as you like!

- `all`: Contains all policies in this repository
- `pod-security-standards-baseline`: Contains policies for the PSS `baseline`
- `pod-security-standards-restricted`: Contains policies for the PSS `restricted`
