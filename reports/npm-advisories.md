# npm Dependency Security Advisory Report — lodash & express

## Audit Header

| Field | Value |
|---|---|
| Prepared for | Dependency Security Review (Monday AM) |
| Prepared by | HeziLiu |
| GitHub login | HeziLiu |
| GitHub account ID | 28861483 |
| Data source | GitHub Global Security Advisory Database (npm ecosystem) |
| Packages in scope | `lodash`, `express` |
| Total advisories found | **17** (lodash: 11, express: 6) |
| High or Critical advisories | **5** — all on lodash (1 critical, 4 high). Express returned none at high/critical severity. |

---

## Executive Summary

- **lodash** carries the bulk of the risk: 11 advisories, including **1 critical** (prototype pollution via `defaultsDeep`) and **4 high** (code injection via `_.template`, command injection via the template function, and two prototype-pollution families). The most recent high-severity issue (GHSA-r5fr-rjxr-66jc, April 2026) affects **all lodash 4.x releases up to and including 4.17.23** — meaning the commonly pinned `4.17.21` is now vulnerable again. First fully patched line is **4.18.0**.
- **express** has no critical or high advisories. Its 6 advisories are 3 medium and 3 low, mostly affecting older lines (express 3.x) or versions patched well before current 4.2x/5.x releases.
- Two advisories in the results set are **withdrawn** (GHSA-8p5q-j9m2-g8wr, GHSA-pj86-cfqh-vqx6) and should be treated as informational only.

### Flagged: Critical & High severity

| GHSA ID | Package | Severity | CVE | Affected versions (npm `lodash`) | First patched |
|---|---|---|---|---|---|
| GHSA-jf85-cpcp-j695 | lodash | **CRITICAL** | CVE-2019-10744 | < 4.17.12 | 4.17.12 |
| GHSA-r5fr-rjxr-66jc | lodash | **HIGH** | CVE-2026-4800 | >= 4.0.0, <= 4.17.23 | 4.18.0 |
| GHSA-35jh-r3h4-6jhm | lodash | **HIGH** | CVE-2021-23337 | < 4.17.21 | 4.17.21 |
| GHSA-p6mc-m468-83gw | lodash | **HIGH** | CVE-2020-8203 | >= 3.7.0, < 4.17.19 | 4.17.19 |
| GHSA-4xc9-xhrj-v574 | lodash | **HIGH** | CVE-2018-16487 | < 4.17.11 | 4.17.11 |

**No express advisory rated high or critical was returned.** The lookup did return advisories for both packages — no empty results.

---

## Package: lodash (11 advisories)

| GHSA ID | Severity | CVE | Summary | Affected versions (npm) | First patched |
|---|---|---|---|---|---|
| GHSA-jf85-cpcp-j695 | **CRITICAL** (CVSS 9.1) | CVE-2019-10744 | Prototype Pollution in `defaultsDeep` | `lodash` < 4.17.12; `lodash-es` < 4.17.14; `lodash-amd` < 4.17.13; `lodash.defaultsdeep` < 4.6.1 | 4.17.12 |
| GHSA-r5fr-rjxr-66jc | **HIGH** (CVSS 8.1) | CVE-2026-4800 | Code Injection via `_.template` `options.imports` key names | `lodash` / `lodash-es` / `lodash-amd` >= 4.0.0, <= 4.17.23; `lodash.template` >= 4.0.0, < 4.18.0 | 4.18.0 |
| GHSA-35jh-r3h4-6jhm | **HIGH** (CVSS 7.2) | CVE-2021-23337 | Command Injection via the template function | `lodash` < 4.17.21; `lodash-es` < 4.17.21; `lodash.template` <= 4.5.0; `lodash-template` <= 1.0.0 | 4.17.21 |
| GHSA-p6mc-m468-83gw | **HIGH** (CVSS 7.4) | CVE-2020-8203 | Prototype Pollution via `pick`, `set`, `setWith`, `update`, `updateWith`, `zipObjectDeep` | `lodash` >= 3.7.0, < 4.17.19; `lodash-es` >= 3.7.0, < 4.17.20; `lodash.pick` >= 4.0.0, <= 4.4.0; `lodash.set` >= 3.7.0, <= 4.3.2; `lodash.setwith` <= 4.3.2; `lodash.update` <= 4.10.2; `lodash.updatewith` <= 4.10.2 | 4.17.19 |
| GHSA-4xc9-xhrj-v574 | **HIGH** (severity high, CVSS not scored) | CVE-2018-16487 | Prototype Pollution via `defaultsDeep`, `merge`, `mergeWith` (`{constructor: {prototype: ...}}`) | `lodash` < 4.17.11 | 4.17.11 |
| GHSA-f23m-r3pf-42rh | MEDIUM (CVSS 6.5) | CVE-2026-2950 | Prototype Pollution via array path bypass in `_.unset` / `_.omit` | `lodash` / `lodash-es` / `lodash-amd` <= 4.17.23; `lodash.unset` >= 4.0.0, < 4.18.0 | 4.18.0 |
| GHSA-xxjr-mmjv-4gpg | MEDIUM (CVSS 6.5) | CVE-2025-13465 | Prototype Pollution in `_.unset` / `_.omit` | `lodash` / `lodash-es` / `lodash-amd` >= 4.0.0, <= 4.17.22; `lodash.unset` >= 4.0.0, <= 4.5.2 | 4.17.23 |
| GHSA-29mw-wpgm-hmr9 | MEDIUM (CVSS 5.3) | CVE-2020-28500 | ReDoS via `toNumber`, `trim`, `trimEnd` | `lodash` / `lodash-es` >= 4.0.0, < 4.17.21; `lodash.trim` / `lodash.trimend` >= 4.0.0, <= 4.5.1 | 4.17.21 |
| GHSA-x5rq-j2xg-h7qm | MEDIUM (CVSS 6.5) | CVE-2019-1010266 | ReDoS via Date handler | `lodash` / `lodash-es` / `lodash-amd` >= 4.7.0, < 4.17.11 | 4.17.11 |
| GHSA-fvqr-27wr-82fm | MEDIUM (CVSS 6.5) | CVE-2018-3721 | Prototype Pollution via `defaultsDeep`, `merge`, `mergeWith` (`__proto__`) | `lodash` < 4.17.5 | 4.17.5 |
| GHSA-8p5q-j9m2-g8wr | LOW — **WITHDRAWN** | CVE-2021-41720 | Arbitrary code execution via template function (disputed, withdrawn by GitHub) | `lodash` <= 4.17.21 (no patched version; advisory withdrawn) | n/a |

### lodash severity breakdown
- Critical: 1
- High: 4
- Medium: 5
- Low: 1 (withdrawn)

### lodash remediation guidance
1. **Upgrade to lodash >= 4.18.0.** This clears every non-withdrawn advisory in the list, including the April 2026 code injection (GHSA-r5fr-rjxr-66jc) and both `_.unset`/`_.omit` prototype pollution issues (GHSA-xxjr-mmjv-4gpg, GHSA-f23m-r3pf-42rh).
2. Note that **4.17.21 — the widely pinned "safe" version — is no longer sufficient**: it is inside the vulnerable range (>= 4.0.0, <= 4.17.23) for GHSA-r5fr-rjxr-66jc and GHSA-f23m-r3pf-42rh.
3. Audit for transitive copies: `lodash-es`, `lodash-amd`, and per-method packages (`lodash.template`, `lodash.unset`, `lodash.defaultsdeep`, `lodash.set`, etc.) are affected independently and may be pulled in by other dependencies.
4. Interim mitigations if 4.18.0 cannot be taken immediately: never pass untrusted input to `_.template` (including `options.imports` key names), and avoid feeding user-controlled property identifiers/paths into `defaultsDeep`, `merge`, `set`, `unset`, `omit`, `pick`, `update`, `zipObjectDeep`.

---

## Package: express (6 advisories)

| GHSA ID | Severity | CVE | Summary | Affected versions (npm) | First patched |
|---|---|---|---|---|---|
| GHSA-cm5g-3pgc-8rg4 | MEDIUM (CVSS 4.0) | CVE-2024-10491 | Resource injection in `response.links` (Link header) | `express` <= 3.21.4 | 4.0.0-rc1 |
| GHSA-rv95-896h-c2vc | MEDIUM (CVSS 6.1) | CVE-2024-29041 | Open Redirect via malformed URLs (`res.location` / `res.redirect`) | `express` < 4.19.2; `express` >= 5.0.0-alpha.1, < 5.0.0-beta.3 | 4.19.2 / 5.0.0-beta.3 |
| GHSA-gpvr-g6gh-9mc2 | MEDIUM (CVSS 6.1) | CVE-2014-6393 | No charset in Content-Type header (XSS via non-standard encodings) | `express` < 3.11.0; `express` >= 4.0.0, < 4.5.0 | 3.11.0 / 4.5.0 |
| GHSA-pj86-cfqh-vqx6 | LOW — **WITHDRAWN** | CVE-2024-51999 | Improperly controlled modification of query properties (extended query parser) — withdrawn as a correctness bug | `express` < 4.22.0; `express` >= 5.0.0, < 5.2.0 | 4.22.0 / 5.2.0 |
| GHSA-qw6h-vgh9-j6wx | LOW (CVSS 5.0) | CVE-2024-43796 | XSS via `response.redirect()` | `express` < 4.20.0; `express` >= 5.0.0-alpha.1, < 5.0.0 | 4.20.0 / 5.0.0 |
| GHSA-jj78-5fmv-mv28 | LOW (CVSS 4.7) | CVE-2024-9266 | Open Redirect (Response object) | `express` >= 3.4.5, < 4.0.0-rc1 | 4.0.0-rc1 |

### express severity breakdown
- Critical: 0
- High: 0
- Medium: 3
- Low: 3 (one withdrawn)

### express remediation guidance
1. **No critical or high findings for express.** Nothing here demands emergency action.
2. Upgrade to **express >= 4.20.0** (or 5.x) to clear every non-withdrawn advisory relevant to modern 4.x/5.x lines: GHSA-qw6h-vgh9-j6wx (XSS via redirect, patched 4.20.0) and GHSA-rv95-896h-c2vc (open redirect, patched 4.19.2).
3. GHSA-cm5g-3pgc-8rg4 and GHSA-jj78-5fmv-mv28 only affect express 3.x — confirm no legacy services are still on 3.x.
4. GHSA-pj86-cfqh-vqx6 is withdrawn (correctness bug, not a vulnerability) but the patched versions (4.22.0 / 5.2.0) also deliver the query-parser hardening if you want it.

---

## Notes on data quality

- Severity levels and version ranges are taken verbatim from the GitHub advisory records.
- Two advisories are marked **withdrawn** upstream (GHSA-8p5q-j9m2-g8wr for lodash, GHSA-pj86-cfqh-vqx6 for express). They are listed for completeness but should not drive remediation decisions.
- GHSA-4xc9-xhrj-v574 is rated "high" by GitHub's advisory severity field but carries no CVSS score in the record.
- Coverage was verified by enumerating all severity levels (critical, high, medium, low, unknown) across non-overlapping publication-date windows for each package, so the counts above should reflect every npm advisory for these two packages in the database.
