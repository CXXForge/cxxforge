# Security Policy

CXXForge treats security as a core engineering requirement, especially because package management and build infrastructure process third-party source code, metadata, and potentially executable build steps.

## Reporting a vulnerability

**Please do not report security vulnerabilities through public GitHub issues or discussions.**

Use GitHub's private vulnerability reporting feature for this repository when available. If that feature is unavailable, contact the maintainers through the private contact method listed in the CXXForge GitHub organization profile.

Include, where possible:

- A concise description of the vulnerability.
- Affected versions, commits, components, and configurations.
- Reproduction steps or a proof of concept.
- Potential impact and known prerequisites.
- Any suggested mitigation.

Do not include unrelated personal data or secrets in a report.

## Coordinated disclosure

Please allow maintainers reasonable time to investigate, validate, and prepare a fix before public disclosure. We will coordinate a disclosure timeline with the reporter and affected parties where practical.

We will acknowledge reports, assess severity, and communicate status as promptly as possible. No response-time guarantee is made at this early project stage.

## Scope

Security reports may concern CXXForge source code, package and registry protocols, dependency resolution, artifact integrity, build execution, credential handling, CI workflows, and official project infrastructure.

Third-party packages or services should be reported to their respective maintainers as well, where appropriate.

## Security design priorities

The project intends to develop explicit policies for package integrity, provenance, signing, dependency auditing, build isolation, credential protection, and vulnerability response. These are design goals, not claims that the capabilities are already implemented.
