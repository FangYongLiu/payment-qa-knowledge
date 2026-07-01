# GLOSSARY · Payment Terms

> Look up any acronym / proper noun here first. Goal: **a newcomer understands it at a glance,
> and an AI resolves it in one grep.**
>
> Two parts: **A. Industry terms** (standard, filled) / **B. Company-internal systems & terms**
> (filled by domain owners — items marked `待补 (TODO)` must NOT be guessed; the person who knows
> gives the authoritative definition).
>
> **To add an entry:** `Term (full name) — one-line definition. Optional expansion.
> → used in: domain / service / flow links`. Also put the acronym in the related object's
> `aliases` so grep finds it. English-first; keep the Chinese business term where useful.

---

## A. Industry terms (standard)

- **MPGS** (Mastercard Payment Gateway Services) — Mastercard's payment gateway; a processing
  channel for card authorization / acquiring / risk. → used in: online-business card acquiring, channel.
- **3DS / 3DS2** (3-D Secure 2.0) — cardholder authentication protocol; the **issuer** verifies the
  cardholder during payment to reduce fraud (may trigger a challenge or be frictionless).
  → used in: online-business, payment-core authorization.
- **DCC** (Dynamic Currency Conversion) — 动态货币转换; a foreign cardholder may pay in their home
  currency. → used in: online-business (e.g. DCC qualification / quotation).
- **MIT / CIT** (Merchant-Initiated / Cardholder-Initiated Transaction) — merchant-initiated (e.g.
  subscription / auto-debit) vs cardholder-initiated. → used in: payment-core (protocol pay), online-business.
- **acquirer / issuer** — 收单机构 / 发卡机构. Acquirer serves the merchant; issuer serves the cardholder.
- **chargeback** — 拒付 / 退单; a cardholder dispute-refund raised via the issuer. → used in: compliance.
- **AML** (Anti-Money Laundering) — 反洗钱. → used in: compliance, risk.
- **KYC** (Know Your Customer) — 实名认证 / identity verification. → used in: kyc.
- **EID** (Emirates ID) — UAE national ID; one KYC document type (the other is Passport). → used in: kyc.
- **liveness / OCR** — 活体核身 / document OCR; key steps in the KYC journey. → used in: kyc.
- **POS** (Point of Sale) — 线下收单终端. → used in: offline-business.
- **IBAN** (International Bank Account Number) — → used in: remittance, wallet fund-out.
- **WPS** (Wage Protection System) — UAE's compliant payroll mechanism (代发工资). → used in: wps.

<!-- Add more industry terms alphabetically / by theme -->

---

## B. Company-internal systems & terms (owners fill; do NOT guess)

> High-frequency internal words that need an authoritative explanation. Lines with `疑似 (likely)`
> are **leads, not facts** — the domain owner must verify, then rewrite as a definition and remove
> the `待补` marker.

- **Xtran** — `待补 (TODO)`. <!-- Explicitly requested; owner to define + where it is used -->
- **DirectPay** — likely: PayBy's online direct-acquiring payment method. `待确认 (verify)` → online-business.
- **tradeii / acquireii / cashierii** — likely: transaction core / acquiring / cashier services
  (`ii` likely = 2nd generation). `待确认` → payment-core / online-business.
- **DPM** — likely: accounting / fund-processing module (see `svc_dpm_accounting` / `dpm_manager` /
  `dpm_task`). `待补`.
- **SGS** — `待补` (internal system full name). <!-- see svc_sgs -->
- **CGS** — `待补` (internal system; the automation suite `cgs-apitest` targets it). <!-- add full name + role -->
- **GRC** — likely: governance / risk / compliance component (see `grc-component-*`). `待确认` → compliance/risk.
- **CKO** — likely: Checkout.com channel / PSP (see `svc_qpay_cko`). `待确认` → channel.
- **VAM** — `待补` (likely virtual account, see `wiki/vam-iban`).
- **BMOC** — `待补` (see `payby-bmoc-operations`).

<!-- New internal terms are added as knowledge is organized; each entry: definition + owning
     domain + links to key service/table. -->
