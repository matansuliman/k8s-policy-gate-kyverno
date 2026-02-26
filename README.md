# Kubernetes Policy-as-Code with Kyverno and GitHub Actions

A small repository demonstrating how to gate pull requests using Kyverno policies.

## Project Structure
- `manifests/`: Contains the Kubernetes applications (Deployments, Services, etc.).
- `policies/`: Contains Kyverno ClusterPolicy definitions.
- `.github/workflows/`: Contains the GitHub Actions test workflow.

## Overview

This project demonstrates how to enforce Kubernetes policy compliance in PRs and branches using Kyverno and GitHub Actions. A workflow runs `kyverno apply` against the `manifests/` directory and fails if any violations are found.

Use this setup as a required GitHub check with branch protection to prevent non-compliant manifests from being merged.

## Local Usage

You can test the policies locally by running the Kyverno CLI:

```bash
kyverno apply policies/ -r manifests/
```

### Seeing it fail

The `manifests/app.yaml` file currently violates the policies intentionally. Running Kyverno locally or opening a PR will result in violations for:
- Usage of the `latest` image tag.
- Missing CPU and Memory requests and limits.
- Missing `runAsNonRoot: true` in the security context.

### Fixing the violations

To fix the deployment so the policy checks pass:
1. Change `nginx:latest` to a specific version (e.g., `nginx:1.24.0`).
2. Add `resources.requests` and `resources.limits` for `cpu` and `memory`.
3. Add `securityContext.runAsNonRoot: true` under the container spec.
