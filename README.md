# Sovereign 🛡️

**The Intent-Aware API Intelligence Engine.**

> *Stop searching for syntax. Start verifying intent.*

---

## 💥 The Problem: Semantic Blindness
We've all been there: you drop a 15MB `swagger.json` file into a generic viewer. It takes 10 seconds to render. You need to verify if any "Public" endpoints are leaking sensitive user data.

*   **Option A (Regex/Grep)**: You search for "password". You get 400 results, mostly from `example: "password123"` in documentation.
*   **Option B (Manual Review)**: You scroll through 2,000 lines of JSON, hoping your eyes don't miss the nested `user_metadata` object.

Both methods are **Syntax-Based**. They check *text*. They don't understand *relationships*.
They can't see that `/v1/profile` (Public) returning `zip_code` + `birth_date` is an Identity Theft vulnerability, while returning `zip_code` alone is harmless.

## 🧠 The Solution: Sovereign
**Sovereign** is a deterministic, client-side intelligence engine. It doesn't just lint your spec; it builds a mental model of your API's **Intent**.

It answers the hard question:
*"This endpoint claims to be public, but why does it return a variable named `session_secret` and require no authentication?"*

### How It Works: The 16-Layer Architecture
Sovereign pipelines your API spec through a multi-stage heuristic engine to distill "Risk" from "Noise".

```mermaid
graph TD
    Input[📄 Raw OpenAPI Spec] --> Layer1
    
    subgraph "Reasoning Core"
    Layer1[Layer 1: Intent Inference 🧠<br/>(Path/Verb/Context Analysis)]
    Layer1 --> Layer3
    Layer3[Layer 3: Semantic Clustering 🧬<br/>(PII & Data Combinations)]
    Layer3 --> Layer14
    Layer14[Layer 14: Constitutional Governance ⚖️<br/>(Policy-as-Code Veto)]
    end
    
    Layer14 --> Layer16
    Layer16[Layer 16: Developer Bridge 🤝<br/>(Human-Readable Remediation)]
    
    Layer16 --> Output[📊 Final Risk Score & Verdict]
    
    style Input fill:#f9f,stroke:#333
    style Output fill:#bbf,stroke:#333
    style Layer14 fill:#fbb,stroke:#f00
```

---

## 🕵️ Logic Preview (Pseudocode)
We don't rely on black-box AI magic. The engine is **deterministic**. Here is a simplified view of the decision loop:

```javascript
function analyzeEndpoint(intent, reality) {
    // 1. Contextual Intent: Does the developer *think* this is safe?
    // e.g. "Get Public Profile"
    
    // 2. Data Semantic Reality: What is *actually* returned?
    // e.g. { "id": "uuid", "dob": "1990-01-01", "mother_maiden_name": "Smith" }
    let sensitivity = detectClusters(reality.schema); 
    // Result: [IDENTITY_LINKABLE, SECURITY_QUESTION_ANSWERS]

    // 3. Constitutional Check (The "Veto")
    if (intent.isPublic && sensitivity.level === 'HIGH') {
        // "I don't care if you marked this 'Safe', you are leaking PII."
        return {
            verdict: 'BLOCK',
            reason: 'CONSTITUTIONAL_BREACH: NO_PUBLIC_PII_LEAKAGE'
        };
    }

    // 4. Architectural Drift Check
    if (endpoint.path.includes('/admin') && !endpoint.hasAuth) {
        return {
            verdict: 'WARN',
            reason: 'BOUNDARY_VIOLATION: UNSECURED_ADMIN_ROUTE'
        };
    }

    return { verdict: 'Clean' };
}
```

---

## ⚡ Comparison: Sovereign vs. The Rest

| Feature | 🔍 Regex / Grep | 📋 Standard Linters (Spectral) | 🛡️ Sovereign Engine |
| :--- | :---: | :---: | :---: |
| **Analysis Type** | Text Patterns | Syntax & Structure | **Semantic Intent** |
| **Privacy** | Local | Local | **Local (In-Browser)** |
| **Context Awareness** | ❌ None | ❌ Single-Field | ✅ **Multi-Signal** |
| **PII Detection** | ⚠️ Keyword Only | ⚠️ Keyword Only | ✅ **Cluster-Based** (A + B = Danger) |
| **Logic** | "Line 40 matches 'admin'" | "Missing description field" | "Public endpoint leaks internal tokens" |

---

## 🎯 Primary Use Cases

### 1. The "Needle in a Haystack" Audit
**Scenario**: You inherit a legacy 500-endpoint API. You have 1 hour to find security holes.
**Sovereign**: Instantly surfaces the 3 endpoints that are Public but return High-Risk data clusters, ignoring the 497 false positives.

### 2. Preventing "Intent Masking"
**Scenario**: A developer names an endpoint `/v1/data/sync` (sounds harmless) but it actually dumps the entire `Users` table including hashed passwords for "debugging".
**Sovereign**: Detects the `password_hash` in the schema and the mass-export behavior, allowing the "Constitution" layer to flag it despite the boring name.

---

## 🗺️ Roadmap
We are just getting started. The logic is robust, but the ecosystem is growing.

- [ ] **Adversarial Pattern Detection**: Catching endpoints that deliberately use obfuscated variables (e.g., `x_val_1` instead of `password`) using entropy analysis.
- [ ] **Visual-Spatial Risk Map**: A 2D force-directed graph showing how data flows between endpoints.
- [ ] **CI/CD Integration**: Headless mode to fail builds if a Constitutional Breach is detected.

---

## 🚦 Project Status
**Current State**: `Private Alpha (v0.6.0)`

This project is under active development. The core **Intent-Aware Engine** is operational and capable of analyzing complex Enterprise specifications.

### Follow the Development
We are building this for engineers who care about **Architecture**, not just Code.
*   ⭐ **Star this repo** to get notified of the public beta.
*   📝 **Issues**: Have a crazy edge case in your Swagger file? Tell us about it.

---
*Built with logic, not just regex.*
