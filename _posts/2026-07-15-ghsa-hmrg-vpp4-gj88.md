---
title: "GHSA-hmrg-vpp4-gj88: authentik Shared Signals Framework access control"
date: 2026-07-15
categories: [security, advisory]
tags: [authentik, authorization, shared-signals-framework, security-research]
---

I reported a Shared Signals Framework authorization issue in authentik, published as **GHSA-hmrg-vpp4-gj88**. The [public advisory](https://github.com/goauthentik/authentik/security/advisories/GHSA-hmrg-vpp4-gj88) credits me as one of the reporters.

## Advisory

- CVE: No known CVE as of September 8, 2026
- GitHub Advisory: `GHSA-hmrg-vpp4-gj88`
- Product: authentik
- Published: July 15, 2026
- Affected versions: `<= 2026.5.4`, `<= 2026.2.5`
- Patched versions: `2026.5.5`, `2026.2.6`
- Severity: Moderate 5.4/10
- CVSS: `CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:N/I:L/A:L`
- CWE: `CWE-862: Missing Authorization`

## Impact

The issue affected Enterprise installations using Shared Signals Framework, with a provider linked as an application's backchannel provider and that application issuing user access tokens. Missing authorization checks on existing streams could compromise the integrity and availability of security event delivery.

Deployments without Shared Signals Framework were not affected. The advisory reports no delivery redirection or disclosure of stored delivery credentials.

## Remediation

The fixes were released in **authentik 2026.5.5 and 2026.2.6**. The advisory lists no workaround and recommends avoiding reliance on Shared Signals Framework event delivery until the deployment is upgraded.
