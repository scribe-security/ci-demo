# Continuous Compliance Platform Demo

This demo repository showcases a continuous compliance platform based on attestations that enables software consumers and producers to transparently demonstrate trust and compliance to secure software development life cycle (SDLC), promote security best practices, meet regulatory requirements, and mitigate cyber risks.

Overview of the Platform
The platform consists of several building blocks that work together to ensure the security and compliance of a supply chain:

# Platform digram 
<img src='img//module_digram.jpg' alt='Platform Digram' width='80%' min-width='600px'/>

<img src='img/platform_table.jpg' alt='Platform table' width='80%' min-width='600px'/>

* Evidence: Immutable objects that contain metadata needed to enable policy enforcement and meet compliance requirements.
* Attestations: Verifiable evidence linked to a specific environmental context, conveying trust using some form of PKI signatures.
* Environmental Context: A labeling system that ties the model together and provides normalized access to many processes of your development process and CI/CD pipeline.
* Policies: A set of user-configured policy modules that define the required compliance report.
Stores: Services providing hosting, upload/download, and querying capabilities for evidence.
* Policy Providers: Entities responsible for signing and providing policy modules.

## Policy Provider example repo
Policy providers can provide OPA based Policy modules.
Modules are signed by provider and can be verified by consumers.
Using the policy modules, consumers can generate compliance reports fitted to the providers regulations.

The following files as an example for a policy module:
* [example.rego](https://github.com/scribe-security/policy-modules/blob/main/modules/example.rego)

> [Releases](https://github.com/scribe-security/policy-modules/releases) include OPA bundle and Signed SLSA Prov by provider.

> [Releases log](https://github.com/scribe-security/policy-modules/actions/workflows/release.yml) for more details.

See https://github.com/scribe-security/policy-modules repo as an example.

## Policy evaluator Repository (This Repository)
Policy evaluation can be run continuously after each release verify compliance as shown by this repo.
Policy evaluation can also happen continuously in an [Admission](https://scribe-security.netlify.app/docs/other-integrations/admission-controller).
Policy evaluation can also happen manually by by CISO as any point.

The following files in this repository are relevant to policy evaluation:
* [.valint.yaml](https://github.com/scribe-security/ci-demo-app/blob/main/.valint.yaml): This file defines the policies and configuration required for a compliance report.
* [.valint_provider](https://github.com/scribe-security/ci-demo-app/blob/main/.valint_provider.yaml): This file specifies the policy provider and verifies the trustworthiness of the policy bundle.

> [Releases](https://github.com/scribe-security/ci-demo-app/releases) include application release assets, and all evidence collected by the compliance requirements.

> [Releases log](https://github.com/scribe-security/ci-demo-app/actions/workflows/release.yaml) for more details.

## Evidence collection
The following evidence is collected during the software supply chain:
* Checkout stage: Signed SBOM. The SBOM includes commits and a graph of what file in your source was edited by what commit.
* Image Release stage: Signed SLSA Prov.
Attached to Github Releases as well as uploaded to Scribe.

## Evaluation
The following checks are performed during compliance evaluation:

* Check that tagged sources are signed.
* Check that the release image is signed.
* Collect an SBOM on sources.
* Collect an SLSA prov on the image.
* Check code owners (who is modifying what part of the SCM).

---
# Demo app💡

This repository shows an end-to-end release management approach for
[Go](https://golang.org/) applications using [Github
Actions](https://github.com/features/actions) as a pipeline for **continuous
integration** (CI), [`goreleaser`](https://goreleaser.com/) for **artifact and
release management**, [`ko`](https://github.com/google/ko) to build OCI-compliant
**container images**, and Kubernetes in Docker
([`kind`](https://github.com/kubernetes-sigs/kind)) for **end-to-end testing**.

## Project Status 🚦

[![Build](https://github.com/scribe-security/ci-demo-app/actions/workflows/build.yaml/badge.svg)](https://github.com/scribe-security/ci-demo-app/actions/workflows/build.yaml)
[![Tests](https://github.com/scribe-security/ci-demo-app/actions/workflows/go-unit-tests.yaml/badge.svg)](https://github.com/scribe-security/ci-demo-app/actions/workflows/go-unit-tests.yaml)
[![Latest Release](https://img.shields.io/github/release/scribe-security/ci-demo-app.svg?logo=github&style=flat-square)](https://github.com/scribe-security/ci-demo-app/releases/latest)
[![Go Report Card](https://goreportcard.com/badge/github.com/scribe-security/ci-demo-app)](https://goreportcard.com/report/github.com/scribe-security/ci-demo-app)
[![codecov](https://codecov.io/gh/scribe-security/ci-demo-app/branch/main/graph/badge.svg?token=TC7MW723JO)](https://codecov.io/gh/scribe-security/ci-demo-app)
[![go.mod Go version](https://img.shields.io/github/go-mod/go-version/scribe-security/ci-demo-app)](https://github.com/scribe-security/ci-demo-app)

## Features 🤩

Based on a trivial Go demo application this repository was built to show the
power of Github Actions and related Go tools with the following highlights:

💫 &nbsp; Add Continuous Integration and **end-to-end release automation** with
[Github Actions](https://github.com/scribe-security/ci-demo-app/actions) ("workflows")  
💫 &nbsp; Add [**status badges**](#project-status-) to your project `README.md`  
💫 &nbsp; **Manage your repository** (issues) and contributions (PRs) with
automatic greetings and code quality checks  
💫 &nbsp; **Produce [artifacts](#artifacts-)** for different platforms and software management
tools, e.g. Homebrew, Snaps, etc.  
💫 &nbsp; **Automate** Github Releases incl. a (templatized) [`CHANGELOG.md`](CHANGELOG.md)  
💫 &nbsp; Use `ko` to **not worry** about building container images and
`Dockerfiles`  
💫 &nbsp; Use `ko` with `kind` for **super fast** development and end-to-end
testing against real APIs (Kubernetes)  

## Artifacts 💎

You can grab the resulting artifacts produced by the Github release
[workflow](./.github/workflows/release.yaml) from the
[releases](https://github.com/scribe-security/ci-demo-app/releases) page.

### Docker 🐳

Multi-arch (platform) Docker images are pushed to Scribe Artifactory as part of the
release pipeline. 
Run the app via `docker`:

```console
$ # expose default port 8080 to 8080 on the Docker host
$ # interrupt with CTRL-C
$ docker run -it --rm -p 8080:8080 scribesecuriy.jfrog.io/scribe-docker-public-local/ci-demo-app:latest
2021-05-04T14:31:00.658Z      INFO    ci-demo-app     ci-demo-app/main.go:85  running server  {"commit": "e616df52", "address": ":8080"}
2021-05-04T14:31:02.933Z      INFO    ci-demo-app     ci-demo-app/main.go:81  got signal, attempting graceful shutdown        {"commit": "e616df52"}
```




















































