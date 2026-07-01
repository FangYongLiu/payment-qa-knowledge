# MAP — Payment System Landscape & Navigation

The entry point to this knowledge base. It gives the whole picture and points to the right domain;
detail lives under each domain. Entries marked `待补` await confirmation by the domain owner.

## The payment system
PayBy is AstraTech's payment platform. It covers online and offline acquiring, wallet and accounts,
remittance / transfer / fund-out, card business, and payroll (WPS). A payment core (transaction,
clearing, reconciliation, accounting) drives it; KYC, risk, and compliance apply throughout; banks
and card schemes are reached through channels.

## Transaction flow (high level)
```
User / merchant initiates
   ↓  acquiring entry
[online-business 线上收单 / offline-business 线下收单]
   ↓  core
[payment-core: transaction (tradeii) → accounting (dpm)]
   ↓  crosscutting checks
[kyc] · [risk] · [compliance / AML]
   ↓  outbound
[channel → banks / card schemes]
   ↓  money movement
[payment-core: clearing / reconciliation]   fund-out → [remittance]   wallet → [wallet]
```
Authoritative service names and DB checkpoints per step live in each domain's `flow/`.

## Business domains
The current working set is below and in `index/domains.yaml`. It is under review and may be revised
through governance.

| Domain | Scope | Entry | Owner |
|---|---|---|---|
| **online-business** | Online acquiring: DirectPay (直连支付), cashier, open/acquiring API | `domains/online-business/` | fangyong.liu |
| **offline-business** | Offline acquiring: POS, scan-to-pay, in-store | `domains/offline-business/` | xiaoqian.wei, wanmei.ding |
| **payment-core** | Core engine: transaction (tradeii), accounting (dpm), clearing/reconciliation, member, GRC | `domains/payment-core/` | xiaoyan.zhou |
| **payment-tools** | Shared payment capabilities: FX/exchange, common services | `domains/payment-tools/` | xiaoyan.zhou |
| **portal-operations** | Merchant portal & ops: onboarding, management, console | `domains/portal-operations/` | yijian.tan |
| **remittance** | Remittance & transfer / fund-out | `domains/remittance/` | lei.pan |
| **wallet** | Wallet & accounts: balance, cash-in, cash-out / withdraw | `domains/wallet/` | qianlong.wang |
| **card** | Card business: prepaid card, issuing / card management | `domains/card/` | jianfei.wang |
| **kyc** | Identity verification: EID / Passport, OCR → liveness → manual review | `domains/kyc/` | xinwei.cao |
| **risk** | Risk control: acs decisioning, risk cases | `domains/risk/` | xinwei.cao, dewen.li |
| **wps** | Payroll — Wage Protection System | `domains/wps/` | xinwei.cao |
| **compliance** | Compliance: AML, chargeback | `domains/compliance/` | dewen.li |
| **channel** | Channel integration: bank / card-scheme channels | `domains/channel/` | 待补 |
| **crypto** | 待补 | `domains/crypto/` | 待补 |
| **marketing** | Marketing: promotions / campaigns | `domains/marketing/` | 待补 |
| **infrastructure** | Infrastructure: gateway, routing, shared components | `domains/infrastructure/` | 待补 |
| **quantix** | 待补 | `domains/quantix/` | Xiaopei.Yan |
| **service-catalog** | Full service/app catalog + call relations | `domains/service-catalog/` | 待补 |

## Where to find things
| Question | Location |
|---|---|
| The businesses / the big picture | this page |
| How a transaction flows / how to verify it | the domain's `flow/` and `scenario/` |
| What a term means | `docs/GLOSSARY.md` |
| A specific service / API / table | the domain's `service/ api/ table/` |
| How to troubleshoot | the domain's `troubleshooting/` |
| Which services/tables a change impacts | domain entry → related objects → `related_*` |
| Coverage | `docs/COVERAGE.md` |
| How to contribute | `docs/KB_ARCHITECTURE.md` |

## Navigation
Read this page, open the domain's `domain_<domain>.md`, then the specific files, following
`related_*` and `[[links]]`. Resolve terms in `docs/GLOSSARY.md`. Grep by the stable prefixes
(`svc_ api_ tbl_ flow_ scn_ ts_`) and `aliases`.
