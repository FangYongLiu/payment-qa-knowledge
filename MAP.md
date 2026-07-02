# MAP — QA Knowledge Base: Landscape & Navigation

The entry point to this knowledge base. It gives the whole picture and points to the right domain;
detail lives under each domain.

Knowledge is organised in two levels: **business line** → **business domain**. Folders mirror this:
`domains/<business-line>/<domain>/`. The registry (`index/domains.yaml`) holds each domain's
`business_line`, owner, and dev_owner. Two business lines:

- **botim-core** — the Botim app: IM, VoIP, Ads, Mini Program.
- **botim-money** — fintech / payment (the PayBy platform). The Botim app wallet is Botim Money
  (PayBy SDK integrated into the app) — the seam between the two lines.

**botim-money** is fully populated; **botim-core** is a skeleton for its teams to fill.

---

# botim-money (Payment / Fintech)

PayBy is AstraTech's payment platform, branded **Botim Money** as a business line. It covers online
and offline acquiring, wallet and accounts, remittance / transfer / fund-out, card business, and
payroll (WPS). A payment core (transaction, clearing, reconciliation, accounting) drives it;
identity/KYC, risk, and compliance apply throughout; banks and card schemes are reached through
channels.

## Transaction flow (high level)
```
User / merchant initiates
   ↓  acquiring entry
[online-business 线上收单 / offline-business 线下收单]
   ↓  core
[payment-core: transaction (tradeii) → accounting (dpm)]
   ↓  crosscutting checks
[activation: identity/KYC] · [risk] · [compliance / AML]
   ↓  outbound
[payment-tool: channels → banks / card schemes]
   ↓  money movement
[settlement: clearing / reconciliation]   fund-out → [fundout / remittance]   wallet → [wallet]
```
Authoritative service names and DB checkpoints per step live in each domain's `flow/`.

## botim-money domains (`domains/botim-money/`)
19 business domains, aligned to owning teams (`index/domains.yaml` holds business_line + owner + dev_owner).

| Domain | Scope | Owner (QA) | Dev team |
|---|---|---|---|
| **online-business** | Online acquiring: ECOM/DirectPay, JSAPI, cashier, open API | fangyong.liu | Merchant Acquiring |
| **offline-business** | Offline acquiring: POS, scan-to-pay, kiosk | xiaoqian.wei, wanmei.ding | Merchant Acquiring |
| **merchant-management** | Merchant onboarding / portal / contract / basis ops / merchant-fundout | yijian.tan | Merchant Portal & Ops |
| **wps** | Payroll (Wage Protection System): company reg, invoice, employees, payroll | xinwei.cao | Merchant Portal & Ops |
| **payment-core** | Core engine: trade, payment, cashier, authpay | xiaoyan.zhou | Payment Core |
| **fundout** | Fund-out | xiaoyan.zhou | Payment Core |
| **deposit-vam** | Fund inflow & virtual accounts: deposit, vis, visii (IBAN), escrow | xiaoyan.zhou | Payment Core |
| **settlement** | Clearing & reconciliation: statementii, settlementii, reconciliation, counter | xiaoyan.zhou | Payment Core (ops: Clearing & Settlement) |
| **infrastructure** | Shared platform: notification, gateway, config, FX rate, ops back-office | xiaoyan.zhou | Payment Core / Dev Ops |
| **crypto** | Crypto-currency: cc-trade/deposit/withdraw/channel, ccdpm, holding | can.wang | Payment Core |
| **payment-tool** | Channel management: CMF, router, adapters, 3DS/DCC, card-BIN | kingo.liang | Payment Tool |
| **wallet** | Wallet & accounts: personal, transfer, deduct, card-binding | qianlong.wang | Wallet |
| **remittance** | Remittance | lei.pan | Remittance |
| **card** | Card issuing (prepaid focus); shared PPC/YSE | jianfei.wang | multi (prepaid → Wallet) |
| **lending** | Lending / BNPL: SNPL, paylater, credit, TTS | Xiaopei.Yan | Quantix |
| **marketing** | Loyalty: promotions, coupons, points | wujiang.ding | Loyalty |
| **activation** | Identity: member + KYC (EID/Passport/OCR/liveness) | xinwei.cao | Activation |
| **risk** | Risk control: GRC, AML, device fingerprint | xinwei.cao, dewen.li | Risk Control |
| **compliance** | Compliance: AML, Edit42, regulatory reporting | dewen.li | Risk Control |

---

# botim-core (Botim App)

The Botim app: instant messaging, voice/video calls, ads, and mini programs. Added by its teams
under the same framework: register the domain in `index/domains.yaml` with `business_line: botim-core`,
create `domains/botim-core/<domain>/` with a `domain_<domain>.md` entry, then fill it per
`templates/README.md`.

## botim-core domains (`domains/botim-core/`)
| Domain | Scope | Owner (QA) | Status |
|---|---|---|---|
| **im** | Instant messaging | 待补 | skeleton |
| **voip** | Voice / video calls (VoIP) | 待补 | skeleton |
| **ads** | Ads | 待补 | skeleton |
| **miniprogram** | Mini programs | 待补 | skeleton |

The **wallet ↔ Botim Money** seam (the app wallet is the PayBy SDK) is documented from the
`botim-money/wallet` side; link across with `[[…]]` when a botim-core flow reaches the wallet.

---

## Meta
`bimo-confirmed` (`business_line: meta`) — confirmed conversation knowledge, not a business domain.

## Where to find things
| Question | Location |
|---|---|
| The business lines / the big picture | this page |
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
