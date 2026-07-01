# MAP · Payment System Landscape & Navigation

> **The single entry point for people and AI.** Read this first to learn what the payment
> system does and which domain to open, then drill down: a domain → `domains/<domain>/
> domain_<domain>.md` (that domain's START HERE). Unknown term → `docs/GLOSSARY.md`.
> Structure & contribution rules → `docs/KB_ARCHITECTURE.md`.
>
> ⚠️ This is a **skeleton**: domain one-liners reflect the current state; items marked
> `待补 (TODO)` are filled by the domain owner — nothing is invented.

## 1. What the payment system does

PayBy is AstraTech's payment platform, covering **online & offline acquiring, wallet & accounts,
remittance / transfer / fund-out, card business, and payroll (WPS)**. It is driven by a
**payment core** (transaction, clearing & settlement, reconciliation, accounting) and runs
**KYC, risk, and compliance** across the flow, connecting to banks / card schemes through
**channels**. <!-- 待补: one authoritative external definition, confirmed by owner -->

## 2. How a transaction flows (high level; details in each domain's `flow/`)

```
User / merchant initiates
   ↓  acquiring entry
[online-business (线上收单) / offline-business (线下收单)]
   ↓  into the core
[payment-core: transaction (tradeii) → accounting (dpm)]
   ↓  crosscutting checks
[kyc 实名] · [risk 风控] · [compliance / AML]
   ↓  outbound
[channel → banks / card schemes]
   ↓  money movement
[payment-core: clearing / reconciliation]   fund-out/transfer → [remittance]   wallet → [wallet]
```
<!-- 待补: authoritative service names + DB checkpoints per step, linked to domains/<domain>/flow/ -->

## 3. The 18 business domains (one line + entry + owner)

| Domain | One line | Entry | Owner |
|---|---|---|---|
| **online-business** | Online acquiring: DirectPay (直连支付), cashier, open/acquiring API, acquiring main flow | `domains/online-business/` | fangyong.liu |
| **offline-business** | Offline acquiring: POS, scan-to-pay (付款码), in-store | `domains/offline-business/` | xiaoqian.wei, wanmei.ding |
| **payment-core** | Core engine: transaction (tradeii), accounting (dpm), clearing/reconciliation, member, GRC — shared base for all business | `domains/payment-core/` | xiaoyan.zhou |
| **payment-tools** | Shared payment capabilities: FX/exchange, common services <!-- 待补 --> | `domains/payment-tools/` | xiaoyan.zhou |
| **portal-operations** | Merchant portal & ops back-office: onboarding, management, console | `domains/portal-operations/` | yijian.tan |
| **remittance** | Remittance & transfer / fund-out | `domains/remittance/` | lei.pan |
| **wallet** | Wallet & accounts: balance, cash-in (充值), cash-out / withdraw (提现) | `domains/wallet/` | qianlong.wang |
| **card** | Card business: prepaid card, issuing / card management | `domains/card/` | jianfei.wang |
| **kyc** | Identity verification (实名认证): EID / Passport, OCR → liveness → manual review | `domains/kyc/` | xinwei.cao |
| **risk** | Risk control: acs decisioning, risk cases | `domains/risk/` | xinwei.cao, dewen.li |
| **wps** | Payroll — Wage Protection System (代发工资) | `domains/wps/` | xinwei.cao |
| **compliance** | Compliance: AML, chargeback (拒付) | `domains/compliance/` | dewen.li |
| **channel** | Channel integration: bank / card-scheme channels (e.g. ENBD, NI, CKO) | `domains/channel/` | 待指派 (unassigned) |
| **crypto** | Crypto-currency related <!-- 待补: scope, confirm with owner --> | `domains/crypto/` | 待指派 |
| **marketing** | Marketing: promotions / campaigns <!-- 待补 --> | `domains/marketing/` | 待指派 |
| **infrastructure** | Infrastructure: gateway, routing, shared components | `domains/infrastructure/` | 待指派 |
| **quantix** | <!-- 待补: likely data/analytics platform — confirm with owner Xiaopei.Yan --> | `domains/quantix/` | Xiaopei.Yan |
| **service-catalog** | Full service/app catalog (282-app inventory) + call relations | `domains/service-catalog/` | 待指派 |

> `bimo-confirmed/` (not a business domain): knowledge confirmed in BimoQA chats and published,
> bucketed by source.

## 4. Where to find what

| You want | Go to |
|---|---|
| What businesses exist / the big picture | this page §1, §3 |
| How a transaction flows / how to verify it | this page §2 → the domain's `flow/` and `scenario/` (steps + DB checkpoints) |
| What a term means (MPGS / Xtran / …) | `docs/GLOSSARY.md` |
| A specific service / API / table | the domain's `service/ api/ table/` |
| How to troubleshoot an issue | the domain's `troubleshooting/` |
| Which services/tables a change impacts | domain entry → related objects → follow `related_*` |
| What's covered vs missing | `docs/COVERAGE.md` |
| How to add/update knowledge correctly | `docs/KB_ARCHITECTURE.md` §6–7 |

## 5. Navigation protocol for AI (read efficiently)

1. Read this `MAP.md` to pick the domain. 2. Read `domains/<domain>/domain_<domain>.md` (its
index) and open only the relevant files. 3. Expand via `related_*` / `[[links]]`. 4. Resolve terms
with `docs/GLOSSARY.md`. 5. Grep with the stable prefixes (`svc_ api_ tbl_ flow_ scn_ ts_`) and
`aliases` (which carry code names / acronyms). **Do not load the whole repo at once.**
