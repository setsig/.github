# Contributing to setsig.com

Thank you for your interest in contributing to the **setsig.com** physical presence and verification ecosystem!

## Ecosystem Structure

- **`setsig-backend`:** Go 1.23+ Core Presence Engine (`api.setsig.com`).
- **`setsig-console`:** Next.js 16 / React 19 Developer Portal (`console.setsig.com`).
- **`setsig-marketing`:** Showcase and documentation (`setsig.com`).
- **`setsig-sdks`:** Official SDKs for React, iOS (Swift), Android (Kotlin), Go, Node.js, and Python.

## Core Rules for Contributors

1. **Zero Unused Variables & Zero Dead Code:**
   - Go: `golangci-lint` must pass with zero issues.
   - TypeScript: `noUnusedLocals: true` and `noUnusedParameters: true` are strictly enforced.
2. **Strict Cryptography & Timing Attacks:**
   - All signature and token comparisons must utilize `crypto/subtle.ConstantTimeCompare` (Go) or equivalent constant-time primitives. Never use standard `==` for hash verification.
3. **Architecture & Integrity Boundaries:**
   - Contributions must preserve the sector-agnostic, non-repudiable presence verification pipeline and must not introduce unlicensed third-party code or weaken cryptographic guarantees.
4. **Sub-15ms Latency Commitment:**
   - The `/v1/sessions/verify` endpoint has a strict p99 < 15ms target. Keep middleware lean and avoid remote network blocking during session verification.

## Development & Testing Workflow

1. Fork the respective repository.
2. Create a feature branch: `git checkout -b feat/your-feature-name`.
3. Ensure all tests and linters pass:
   - Go: `go test -v ./...`
   - TypeScript: `npx tsc --noEmit && npm run lint`
   - Python: `python3 -m unittest discover tests`
4. Submit a Pull Request with a clear description and testing evidence.

