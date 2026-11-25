<div align="center">

# `setsig.com`
### Physical Presence & Verification Infrastructure-as-a-Service (PaaS/IaaS)

[![Engine Status](https://img.shields.io/badge/Core%20Engine-Go%201.23%2B-00ADD8?style=flat-square&logo=go)](https://api.setsig.com/v1/health)
[![Verification Latency](https://img.shields.io/badge/p99%20Latency-%3C%2015ms-10B981?style=flat-square)](https://setsig.com)
[![Hardware Attestation](https://img.shields.io/badge/Attestation-App%20Attest%20%2F%20Play%20Integrity-6366F1?style=flat-square)](https://setsig.com/technology)
[![Visual Proof](https://img.shields.io/badge/Visual%20Proof-Cryptographic%20Evidence%20Chain-F59E0B?style=flat-square)](https://setsig.com/technology)
[![Double-Entry Ledger](https://img.shields.io/badge/Billing-Double--Entry%20Ledger-3B82F6?style=flat-square)](https://console.setsig.com)
[![License](https://img.shields.io/badge/License-Apache%202.0%20%2F%20Proprietary%20Core-zinc?style=flat-square)](./LICENSE)

<br />

**Mathematical and Cryptographic Certainty for Physical Presence Verification.**  
Eliminating location spoofing, proxy check-ins, remote screenshot attacks, and hardware emulation across mission-critical B2B workflows.

[**Explore Platform**](https://setsig.com) • [**Developer Console**](https://console.setsig.com) • [**API Reference**](https://setsig.com/docs) • [**Status & Uptime**](https://status.setsig.com)

</div>

---

## 🏛️ What is setsig?

In an era of simulated software, mock locations, remote screen shares, and synthetic camera feeds, standard applications cannot trust client GPS or static QR codes. 

**setsig** answers a single question with non-repudiable mathematical proof:  
> *"Was this specific user physically present at this exact venue at this exact second?"*

By unifying **Dynamic TOTP (RFC 6238)**, **Spherical Haversine Geofencing**, **Hardware-Backed Device Attestation (Apple Secure Enclave & Google Play Integrity)**, and **Cryptographic Visual Evidence Chain**, setsig provides an enterprise-grade verification orchestrator that responds in **sub-15 milliseconds (p99)**.

---

## 🛡️ Multi-Layer Defense in Depth

```
                                  [ Physical Venue Terminal ]
                                              │
                         ┌────────────────────┴────────────────────┐
                         ▼                                         ▼
                 [ Dynamic TOTP QR ]                       [ Device Scanner ]
                 (30-60s RFC 6238 Seed)                   (GPS + Hardware Token)
                         │                                         │
                         └────────────────────┬────────────────────┘
                                              ▼
                                 [ setsig Core Engine ]
                            (Go 1.23+ / Chi / Goroutines)
                                              │
              ┌───────────────────────────────┼───────────────────────────────┐
              ▼                               ▼                               ▼
       [ Haversine Math ]           [ Atomic Double-Spend ]         [ Hardware Attestation ]
     (Float64 Radius Check)           (Redis 7.4 SETNX 120s)         (Apple / Play Integrity)
              │                               │                               │
              └───────────────────────────────┼───────────────────────────────┘
                                              ▼
                                  [ Proof-of-Presence ]
                          (Immutable Audit Log / Webhook Event)
```

1. **Ephemeral Dynamic TOTP (30-60s):** Dynamic QR tokens auto-refresh using venue seeds. Screenshots, photos, and forward relays become useless within seconds.
2. **Haversine Geofencing:** Mathematical distance checks against venue radius (`10m <= radius <= 250m`) computed in nanoseconds without third-party GPS lookup bottlenecks.
3. **Hardware-Backed Telemetry (Zero-Trust):** Integration with Apple App Attest and Google Play Integrity API to cryptographically certify that client requests originate from genuine unrooted physical devices.
4. **Cryptographic Visual Evidence Chain:** Two-stage intent handshake with a 10-second live capture window, direct cloud storage upload, and SHA-256 HMAC session sealing, preventing virtual camera injection.
5. **Two-Layer Replay Protection:**
   - Layer 1: Sub-millisecond Redis distributed atomic lock (`SETNX setsig:lock:token:{id} 1 EX 120`).
   - Layer 2: PostgreSQL TimescaleDB append-only ledger constraint (`CONSTRAINT uq_session_tenant_client_token UNIQUE (tenant_id, client_token)`).

---

## 📦 Official SDK Ecosystem

All official client libraries and SDKs are strictly versioned, type-safe, and compatible with modern runtimes:

| Ecosystem | Package / Library | Description | Repository |
| :--- | :--- | :--- | :--- |
| **React / Next.js** | [`@setsig/react`](https://www.npmjs.com/package/@setsig/react) | React 18 & 19 hooks and RSC-safe components with zero hydration mismatch | [`setsig-sdks/react`](https://github.com/setsig/setsig-sdks/tree/main/react) |
| **iOS / Swift** | [`SetsigSDK`](https://github.com/setsig/setsig-sdks/tree/main/ios) | Swift Package Manager (iOS 15+) with Apple App Attest & SwiftUI Kiosk | [`setsig-sdks/ios`](https://github.com/setsig/setsig-sdks/tree/main/ios) |
| **Android / Kotlin** | [`setsig-android`](https://github.com/setsig/setsig-sdks/tree/main/android) | Kotlin coroutines client, Google Play Integrity helper & Jetpack Compose Kiosk | [`setsig-sdks/android`](https://github.com/setsig/setsig-sdks/tree/main/android) |
| **Go** | [`setsig-go`](https://pkg.go.dev/github.com/setsig/setsig-go) | Idiomatic Go 1.23+ client with built-in retries and HMAC verification | [`setsig-sdks/go`](https://github.com/setsig/setsig-sdks/tree/main/go) |
| **Node.js** | [`@setsig/node`](https://www.npmjs.com/package/@setsig/node) | Type-safe TypeScript / Node.js ESM client with webhook verification | [`setsig-sdks/node`](https://github.com/setsig/setsig-sdks/tree/main/node) |
| **Python** | [`setsig`](https://pypi.org/project/setsig/) | Python 3.10+ client with dataclasses and cryptographic helpers | [`setsig-sdks/python`](https://github.com/setsig/setsig-sdks/tree/main/python) |
| **Browser / Web** | [`@setsig/browser`](https://www.npmjs.com/package/@setsig/browser) | Web client with geolocation watch & Web Crypto SHA-256 | [`setsig-sdks/browser`](https://github.com/setsig/setsig-sdks/tree/main/browser) |
| **Edge CDN** | `setsig-kiosk.js` | Zero-dependency standalone script embed for kiosk tablets | `https://cdn.setsig.com/kiosk/setsig-kiosk.js` |

---

## ⚡ Quickstart

### 1. Embed Dynamic Kiosk QR in React / Next.js

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
        VenueID:     "ven_ist_airport_gate_04",
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

// Generate hardware attestation token from Apple Secure Enclave
let attestationToken = try await AppAttestService.shared.generateAttestation(
    clientToken: "usr_99182",
    challenge: scannedTokenId
)

let result = try await client.verifyPresence(request: VerifySessionRequest(
    venueId: "ven_ist_001",
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

## 🏢 Platform Repositories

| Repository | Responsibility | Stack |
| :--- | :--- | :--- |
| **[`setsig-backend`](https://github.com/setsig/setsig-backend)** | Core Verification Engine, REST API, Webhooks & Ledger | Go 1.23+, Chi, Redis 7.4 Cluster, PostgreSQL 16 (TimescaleDB) |
| **[`setsig-console`](https://github.com/setsig/setsig-console)** | B2B Partner Portal, Venue Management, Analytics & RBAC | Next.js 16, React 19, Tailwind CSS v4, CVA, TanStack Query v5 |
| **[`setsig-marketing`](https://github.com/setsig/setsig-marketing)** | Public Showcase, Playground, Global Documentation & Blog | Next.js 16, `next-intl` (en, tr, de, ar), True-Black UI |

---

## 🔒 Security & Vulnerability Reporting

Security is central to our mission. If you discover a security vulnerability within setsig infrastructure or SDKs, please review our [Security Policy](./SECURITY.md) and disclose it responsibly to:

📧 **`security@setsig.com`**

Please do not open public issues for sensitive security vulnerabilities. We offer prompt remediation and recognition via our coordinated disclosure process.

---

## 📜 Governance & Enterprise Licensing

- Core verification algorithms, mathematical geofencing models, and cryptographic visual evidence pipelines are proprietary technologies operated by **setsig.com**.
- Platform operations are governed under **AVCI Ventures**.
- For licensing, enterprise on-premise deployments, or custom defense/aviation integration, contact [enterprise@setsig.com](mailto:enterprise@setsig.com).

---

<div align="center">
<sub>© 2026 setsig.com — Infrastructure by AVCI Ventures. All rights reserved.</sub>
</div>

