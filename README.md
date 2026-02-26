# Kubernetes Policy-as-Code with Kyverno and GitHub Actions

A small repository demonstrating how to gate pull requests using Kyverno policies.

## Project Structure
- `manifests/`: Contains the Kubernetes applications (Deployments, Services, etc.).
- `policies/`: Contains Kyverno ClusterPolicy definitions.
- `.github/workflows/`: Contains the GitHub Actions test workflow.
