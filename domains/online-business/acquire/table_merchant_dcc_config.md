---
id: tbl_merchant_dcc_config
object_type: Table
name: "t_merchant_dcc_config (商户 DCC 配置表)"
aliases: ["t_merchant_dcc_config", "商户DCC配置", "DCC配置", "MID-level DCC", "markupRate", "rebateRate", "currency blacklist", "currency whitelist"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: Arpit
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO 02_DCC_Product_Config TC14-TC17; markup/rebate validation TC04-TC11"
tags: ["config", "DCC", "markup", "rebate", "currency"]
related_services: ["svc_acquireii"]
related_tables: ["tbl_acquireii_t_acquire_order"]
related_logs: ["service:acquireii"]
---

## 用途
商户 DCC 配置:provider、币种白/黑名单、MID 级 vs 默认配置、markup/rebate 费率(费率最终落 pricing 表 `pbsdb.tb_pbs_price_cal` / `tb_pbs_price_strategy_param`)。

## 配置优先级
- `t_merchant_dcc_config` 含 MID 级数据 → 用 MID 级配置(TC14)。
- 无 MID 级、仅默认配置 → 用默认配置(TC15)。
- UI 更新走审核,落 `t_merchant_dcc_config` + `t_merchant_dcc_config_audit`(TC16)。

## 费率取值校验规则(markup / rebate)
- 取值范围:`0 < rate < 1`,否则报 "Rate should be greater than 0 and less than 1"。
- `rebateRate` 不得大于 `markupRate`,否则拒绝。
- 最多 4 位小数(0.1234 接受;0.12345 截断/报错)。

## 产品开通/关闭
- 开通 BPG/DirectPay DCC 经 basis-merchant 申请 + 审核;落 `ppcenter.t_product_apply_order(S)` / `t_merchant_product_order(S)` + pricing 表。
- 关闭后新交易不再触发 DCC(即时生效)。

## 常见问题
- provider≠CKO 导致 DCC 不可用;费率超界/小数位超 4;MID 级与默认配置取错。
