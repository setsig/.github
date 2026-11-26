<div align="center">

# `setsig.com`
### Physical Presence & Verification Infrastructure

[![Verification Latency](https://img.shields.io/badge/Engine%20Target-p99%20%3C%2015ms-10B981?style=flat-square)](https://setsig.com)
[![Hardware Attestation](https://img.shields.io/badge/Attestation-App%20Attest%20%2F%20Play%20Integrity-6366F1?style=flat-square)](https://setsig.com/technology)
[![Visual Proof](https://img.shields.io/badge/Visual%20Proof-Cryptographic%20Evidence%20Chain-F59E0B?style=flat-square)](https://setsig.com/technology)
[![License](https://img.shields.io/badge/License-Apache%202.0%20SDKs-zinc?style=flat-square)](./LICENSE)

<br />

**Mathematical and Cryptographic Certainty for Physical Presence Verification.**  
Eliminating location spoofing, proxy check-ins, remote screenshot attacks, and hardware emulation across mission-critical B2B workflows.

[**Explore Platform**](https://setsig.com) • [**Developer Console**](https://console.setsig.com) • [**API Reference**](https://setsig.com/docs) • [**Integrations**](https://setsig.com/integrations)

</div>

---

## What is setsig?

In an era of simulated software, mock locations, remote screen shares, and synthetic camera feeds, standard applications cannot trust client GPS or static QR codes.

**setsig** answers a single question with non-repudiable cryptographic proof:
> *"Was this specific user physically present at this exact venue at this exact second?"*

By unifying **Dynamic TOTP (RFC 6238)**, **Spherical Geofencing**, **Hardware-Backed Device Attestation**, and **Cryptographic Visual Evidence Chain**, setsig provides an enterprise-grade verification platform engineered for **sub-15 millisecond (p99)** response times.

---

## Multi-Layer Security Guarantees

1. **Ephemeral Dynamic TOTP (30–60s):** Rotating QR payloads invalidate screenshots, forwarded photos, and remote relays within seconds.
2. **Precision Geofencing:** Real-time distance verification against configurable physical venue boundaries.
3. **Hardware-Backed Device Integrity:** Cryptographic device attestation supporting Apple App Attest and Google Play Integrity.
4. **Cryptographic Visual Evidence Chain:** Two-stage live capture handshake (10s window) with SHA-256 digest binding and HMAC session sealing.
5. **Distributed Single-Use Replay Protection:** Atomic single-use token locking combined with an immutable append-only verification ledger prevents double-spend and replay attacks.

---

## Official SDK Ecosystem

All official client libraries are strictly versioned, type-safe, and ready for production:

| Ecosystem | Package / Library | Description | Repository |
| :--- | :--- | :--- | :--- |
| **React / Next.js** | [`@setsig/react`](https://www.npmjs.com/package/@setsig/react) | React 18 & 19 hooks and RSC-safe components | [`setsig-skds-react`](https://github.com/setsig/setsig-skds-react) |
| **iOS / Swift** | [`SetsigSDK`](https://github.com/setsig/setsig-skds-ios) | Swift Package Manager (iOS 15+) with Apple App Attest & SwiftUI Kiosk | [`setsig-skds-ios`](https://github.com/setsig/setsig-skds-ios) |
| **Android / Kotlin** | [`setsig-android`](https://github.com/setsig/setsig-skds-android) | Kotlin coroutines client, Google Play Integrity helper & Compose Kiosk | [`setsig-skds-android`](https://github.com/setsig/setsig-skds-android) |
| **Go** | [`setsig-go`](https://pkg.go.dev/github.com/setsig/setsig-go) | Idiomatic Go client with retries and constant-time HMAC verification | [`setsig-skds-go`](https://github.com/setsig/setsig-skds-go) |
| **Node.js** | [`@setsig/node`](https://www.npmjs.com/package/@setsig/node) | Type-safe TypeScript / Node.js ESM client with webhook verification | [`setsig-skds-node`](https://github.com/setsig/setsig-skds-node) |
| **Python** | [`setsig`](https://pypi.org/project/setsig/) | Python 3.10+ zero-dependency client with cryptographic helpers | [`setsig-skds-python`](https://github.com/setsig/setsig-skds-python) |
| **Browser / Web** | [`@setsig/browser`](https://www.npmjs.com/package/@setsig/browser) | Web client with geolocation & Web Crypto SHA-256 | [`setsig-skds-browser`](https://github.com/setsig/setsig-skds-browser) |

---

## E-Commerce & No-Code Integrations

Launch physical check-in verification for workshops, events, and venues in minutes without custom backend code:

| Platform | Integration | Setup | Access |
| :--- | :--- | :--- | :--- |
| **WooCommerce** | WordPress HPOS Plugin, Admin Metabox & Shortcodes | ~3 min | [`setsig-woocommerce`](https://github.com/setsig/setsig-woocommerce) |
| **Shopify** | Order Status & POS UI Extensions, GraphQL Sync & GDPR | ~2 min | [`setsig-shopify`](https://github.com/setsig/setsig-shopify) |
| **ikas** | OAuth App, Branch-to-Venue Sync & Embedded Kiosk | ~2 min | [`setsig-ikas`](https://github.com/setsig/setsig-ikas) |
| **Shopier** | Managed Webhook Connector & Evidence Pack | ~5 min | [Console Integrations](https://console.setsig.com/integrations) |

---

## Quickstart

### 1. Embed Dynamic Kiosk QR (React / Next.js)

```tsx
"use client";

import { SetsigQRCode } from "@setsig/react";

export function GateTerminal({ venueId }: { venueId: string }) {
  return (
    <SetsigQRCode
      venueId={venueId}
      apiKey="pk_live_..."
      refreshInterval={60}
      size={260}
      onRefresh={(token) => console.log("New dynamic token:", token.tokenId)}
    />
  );
}
```

### 2. Verify Presence on Backend (Go)

```go
package main

import (
    "context"
    "fmt"
    "github.com/setsig/setsig-go"
)

func main() {
    client := setsig.NewClient("sk_live_...")

    session, err := client.Sessions.Verify(context.Background(), &setsig.VerifySessionRequest{
        VenueID:     "ven_gate_04",
        TokenID:     scannedTokenID,
        ClientToken: "usr_pass_8819",
        Latitude:    41.2753,
        Longitude:   28.7519,
        Accuracy:    4.5,
    })
    if err != nil {
        panic(err)
    }

    fmt.Printf("Presence Verified! Distance: %.2fm, Status: %s\n", session.DistanceMeters, session.Status)
}
```

### 3. Native iOS Presence Attestation (Swift)

```swift
import SetsigSDK

let client = SetsigClient(apiKey: "pk_live_...")

let attestationToken = try await AppAttestService.shared.generateAttestation(
    clientToken: "usr_99182",
    challenge: scannedTokenId
)

let result = try await client.verifyPresence(request: VerifySessionRequest(
    venueId: "ven_gate_01",
    tokenId: scannedTokenId,
    clientToken: "usr_99182",
    latitude: 41.0082,
    longitude: 28.9784,
    accuracy: 3.5,
    attestationToken: attestationToken
))

print("Verified: \(result.status), Distance: \(result.distanceMeters)m")
```

---

## Security & Vulnerability Reporting

Security is central to our mission. If you discover a security vulnerability within setsig services, SDKs, or integrations, please review our [Security Policy](./SECURITY.md) and disclose it responsibly to:

**`security@setsig.com`**

Please do not open public issues for sensitive security vulnerabilities.

---

## Governance & Enterprise Licensing

- Core verification services and cryptographic visual evidence pipelines are operated by **setsig.com** under **AVCI Ventures**.
- For enterprise deployments, custom SLAs, or volume licensing, contact [enterprise@setsig.com](mailto:enterprise@setsig.com).

---

<div align="center">
<sub>© 2026 setsig.com — AVCI Ventures. All rights reserved.</sub>
</div>
