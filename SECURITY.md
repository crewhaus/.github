# Security Policy

This policy applies to every repository in the [crewhaus](https://github.com/crewhaus) GitHub organization. CrewHaus takes security seriously; vulnerability reports get priority response.

## Reporting a vulnerability

**Do not file a public GitHub issue.**

Instead, email **security@crewhaus.ai** with:

- A description of the vulnerability
- Steps to reproduce
- Affected versions, if known
- Your assessment of severity
- Whether you've disclosed this to anyone else
- How you'd like to be credited (or kept anonymous)

We will acknowledge receipt within **3 business days**. We aim to provide an initial assessment within **7 business days**, including:

- Whether we can reproduce it
- Our initial severity rating
- An expected timeline for fix

## Supported versions

| Version | Status |
|---|---|
| 0.x (current) | Active — security fixes ship in patch releases |
| Pre-1.0 versions | Best-effort. We backport critical fixes when feasible. |

Once we hit 1.0, we will publish a formal support window (likely "current major + previous major for 6 months").

## Scope

This policy covers:

- All repositories in the crewhaus GitHub organization
- `@crewhaus/cli`, `@crewhaus/core`, `@crewhaus/runtime-core` and all other published `@crewhaus/*` npm packages
- The compiler and target emitters in [`crewhaus/factory`](https://github.com/crewhaus/factory)
- The `crewhaus.ai` website, plus `docs.crewhaus.ai`, `forge.crewhaus.ai`, and `cloud.crewhaus.ai` once those properties are live

This policy does NOT cover:

- Third-party community artifacts. Report security issues in community artifacts directly to their authors.
- Issues in your own usage of CrewHaus (e.g., your own secrets handling). Those are deployment concerns, not CrewHaus vulnerabilities.
- Vulnerabilities in upstream dependencies — report those to the upstream maintainer. We will respond to dependency-chain vulnerabilities by upgrading.

## What we consider a vulnerability

- Code execution via crafted spec.yaml or artifact input
- Authentication / authorization bypass in a hosted CrewHaus service, once one is offered
- Bypass of the boundary classifier (prompt injection sneaking past `TrustOrigin` classification)
- Information disclosure (secrets, customer data, eval results)
- Denial of service that goes beyond "the model is slow"
- Supply-chain attacks (compromised dependencies, malicious typosquats)

We treat the boundary classifier as a critical component. If you find an input that should classify as malicious or suspicious but classifies as safe, that's a vulnerability worth reporting.

## What we do not consider a vulnerability

- The model itself producing low-quality or undesirable output. CrewHaus is not responsible for model behavior; it's responsible for safe orchestration around the model.
- Configuration issues in your own deployment.
- DoS via legitimately-expensive operations (e.g., a spec that calls the model 10,000 times). These are usage concerns; we provide budgeting hooks but don't enforce limits.

## Disclosure

We coordinate disclosure with you:

1. We confirm the vulnerability
2. We develop and test a fix
3. We notify any known affected users (if there's an active customer relationship)
4. We release the fix
5. We publish a GitHub Security Advisory with credit (or anonymity, per your preference)

Target timeline from report to disclosure: **30-90 days** depending on severity and complexity. We will request an extension if needed and keep you informed.

## Safe harbor

We will not pursue legal action against security researchers who:

- Report vulnerabilities to security@crewhaus.ai before public disclosure
- Do not access data they don't need to demonstrate the vulnerability
- Do not disrupt our services beyond what's necessary to demonstrate
- Give us reasonable time to fix before public disclosure (typically 30-90 days)

Good-faith security research is welcome.

## Hall of fame

Researchers who have responsibly disclosed vulnerabilities to us are credited here (with their consent):

*(none yet — be the first)*

## PGP

If you need to encrypt your report, our PGP key is at https://crewhaus.ai/.well-known/security.txt (once the website is live).

## Bug bounty

We do not currently offer a paid bug bounty. We may offer one in the future for CrewHaus Cloud once it has paying customers. For now, recognition (the hall of fame above) and our gratitude are what we can offer.

---

*Last updated: 2026-06-10*
