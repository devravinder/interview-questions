# Testing, DevOps and Production: Basic to Advanced

Read these first; this file adds only what they don't cover:

- [DevOps questions](questions.md): Git, Docker, Kubernetes components, Terraform vs Ansible
- [Senior developer topics](../system-design/senior-dev.md): contract testing, Testcontainers, load and chaos testing, SLOs, postmortems
- [Java questions](../java/questions.md): observability stack, CI pipeline values

## Basic

1. Unit vs integration vs end-to-end tests? What is the test pyramid?
2. Mocks vs stubs vs fakes?
3. What is TDD? When do you use it and when not?
4. What is a multi-stage Dockerfile and why use it?
   - Build in one stage and copy only the output to a small runtime image.

## Intermediate

1. How do you keep tests fast and not flaky?
   - No sleeps, no shared state between tests, fixed clocks and seeds, and real dependencies in containers instead of shared test servers.
2. Kubernetes requests vs limits for CPU and memory?
   - The scheduler uses requests. A container is CPU-throttled at its CPU limit and OOM-killed at its memory limit.
3. How does a rolling update work and how do you roll back?
   - `maxSurge` and `maxUnavailable` control the pace; `kubectl rollout undo` goes back to the last revision.
4. What do you alert on?
   - Symptoms users feel (error rate, latency, saturation), not every CPU spike.

## Advanced

1. Horizontal Pod Autoscaler: what does it scale on and what are the pitfalls?
   - CPU, memory or custom metrics. Pitfalls: slow startup, missing requests, and scaling the app beyond what the DB can take.
2. GitOps: what is it? (Argo CD, Flux)
3. How do you manage secrets in Kubernetes?
   - External Secrets with a cloud secret manager or Vault. Kubernetes secrets are only Base64-encoded unless encryption at rest is on.
4. What is the OpenTelemetry Collector and why use it?
   - One agent receives logs, metrics and traces, then batches, filters and exports them to any backend.

## Scenario

1. Pods restart with `OOMKilled` but the heap looks fine. What else uses memory?
2. The pipeline takes 40 minutes. How do you bring it under 10?
3. A deploy went out with a bug that corrupts data. Walk through your response.
