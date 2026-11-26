# Contributing to setsig.com

Thank you for your interest in contributing to the **setsig.com** SDK and integration ecosystem!

## Open-Source Ecosystem

- **Official SDKs:** React, iOS (Swift), Android (Kotlin), Go, Node.js, Python, and Browser.
- **E-Commerce Integrations:** WooCommerce, Shopify, ikas, and Shopier.

## Core Rules for Contributors

1. **Zero Unused Variables & Zero Dead Code:**
   - Strict compiler and linter rules must pass with zero warnings or dead code.
2. **Strict Cryptography & Timing Attacks:**
   - All signature and token comparisons must use constant-time primitives (`crypto/subtle.ConstantTimeCompare`, `crypto.timingSafeEqual`, `hash_equals`, `hmac.compare_digest`). Never use standard `==` for hash verification.
3. **Architecture & Integrity Boundaries:**
   - Contributions must preserve the sector-agnostic, non-repudiable presence verification contract and must never embed secret keys (`sk_live_`) in client-side code.
4. **Low-Latency Commitment:**
   - Keep SDK and plugin middleware lean and avoid blocking calls during presence verification.

## Development & Testing Workflow

1. Fork the respective repository.
2. Branch from `dev`: `git checkout -b feat/your-feature-name dev`.
3. Ensure all tests and linters pass before opening a Pull Request into `dev`.
