# Security Policy — setsig.com

setsig.com takes the security and integrity of physical presence verification seriously. We appreciate responsible disclosure of any vulnerabilities found across our backend engines, APIs, mobile SDKs, or developer portals.

## Supported Versions

| Version / Component | Supported | Release Channel |
| :--- | :--- | :--- |
| Core Engine (`setsig-backend`) | :white_check_mark: | Go 1.23+ (`api.setsig.com`) |
| Developer Console (`setsig-console`) | :white_check_mark: | Next.js 16 (`console.setsig.com`) |
| Global SDKs (`@setsig/react`, `SetsigSDK`, `setsig-android`, `setsig-go`, `@setsig/node`, `setsig-python`) | :white_check_mark: | npm, SPM, Maven, Go Proxy, PyPI |

## Reporting a Vulnerability

**DO NOT file a public GitHub issue for security vulnerabilities.**

Instead, please send an encrypted or standard email report to:
📧 **`security@setsig.com`**

Include:
1. Type of issue (e.g. timing-attack bypass, double-spend replay, attestation forgery, geofence escape).
2. Step-by-step reproduction instructions or Proof-of-Concept (PoC) code.
3. Affected SDK, API endpoint, or component.
4. Expected vs. observed cryptographic or mathematical behavior.

## SLA & Response Commitment

- **Acknowledgment:** Within 24 hours.
- **Initial Severity Triage:** Within 48 hours.
- **Remediation & Patch Deployment:** Critical vulnerabilities are addressed within 72 hours under an expedited hotfix protocol.
- **Credit:** We credit security researchers in our release notes unless anonymity is preferred.
