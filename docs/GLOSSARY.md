# Glossary

Terminology for the systems the QA team covers. Section A covers industry-standard terms; Section B
covers internal systems. Entries marked `待补` await an authoritative definition from the domain owner and
must not be guessed. Entry format: `Term (full name) — definition. → used in: domain/service`.

## A. Industry terms
- **MPGS** (Mastercard Payment Gateway Services) — Mastercard's payment gateway; a processing
  channel for card authorization and acquiring. → used in: online-business, payment-tool.
- **3DS / 3DS2** (3-D Secure 2.0) — cardholder authentication in which the issuer verifies the
  cardholder during payment; may be a challenge or frictionless. → used in: online-business, payment-core.
- **DCC** (Dynamic Currency Conversion) — a foreign cardholder may pay in their home currency.
  → used in: online-business.
- **MIT / CIT** (Merchant-Initiated / Cardholder-Initiated Transaction) — merchant-initiated (e.g.
  subscription, auto-debit) versus cardholder-initiated. → used in: payment-core, online-business.
- **acquirer / issuer** — the merchant's bank / the cardholder's bank.
- **chargeback** — a cardholder dispute-refund raised through the issuer. → used in: compliance.
- **AML** (Anti-Money Laundering) — → used in: compliance, risk.
- **KYC** (Know Your Customer) — customer identity verification. → used in: kyc.
- **EID** (Emirates ID) — UAE national ID; a KYC document type (with Passport). → used in: kyc.
- **liveness / OCR** — liveness detection / document recognition, steps in the KYC journey. → used in: kyc.
- **POS** (Point of Sale) — offline acquiring terminal. → used in: offline-business.
- **IBAN** (International Bank Account Number) — → used in: remittance, wallet.
- **WPS** (Wage Protection System) — the UAE's compliant payroll mechanism. → used in: wps.

## B. Internal systems
- **DirectPay** — `待补`. Likely PayBy's online direct-acquiring payment method. → online-business.
- **tradeii / acquireii / cashierii** — `待补`. Likely the transaction-core / acquiring / cashier
  services. → payment-core, online-business.
- **DPM** — `待补`. Accounting / fund-processing module (`svc_dpm_*`).
- **SGS** — `待补` (`svc_sgs`).
- **CGS** — `待补`.
- **GRC** — `待补`. Governance / risk / compliance component (`grc-component-*`).
- **CKO** — `待补` (`svc_qpay_cko`).
- **VAM** — `待补`.
- **BMOC** — `待补`.
