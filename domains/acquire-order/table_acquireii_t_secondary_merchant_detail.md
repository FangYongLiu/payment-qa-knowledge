---
id: tbl_acquireii_t_secondary_merchant_detail
object_type: Table
domain: acquire-order
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_secondary_merchant_detail.md
tags:
- 二级商户
- 聚合支付
- MCC
subdomain: null
module: null
sensitivity: normal
name: 二级商户明细表
aliases:
- t_secondary_merchant_detail
- acquireii.t_secondary_merchant_detail
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录订单中的二级商户信息，用于聚合支付、SaaS 平台场景。

- 一级商户：直接和支付公司签约的商户
- 二级商户：通过一级商户接入的下游商户（如平台上的店铺）

表名 `acquireii.t_secondary_merchant_detail`，与 `t_acquire_order` 1:1 关联（通过 `global_id`）。

## 关键列
| 字段 | 类型 | 说明 |
|------|------|------|
| `global_id` | bigint | 主键，对应订单 global_id |
| `mcc` | varchar(32) | MCC（商户类别码） |
| `name` | varchar(255) | 商户名 |
| `merchant_id` | varchar(64) | 商户 ID（业务标识） |
| `merchant_inner_id` | bigint | 二级商户内部 ID |

## 主键/索引
| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |
| `idx_smd_id` | merchant_id | 按商户查 |

## 校验点(QA 关注)
1. **MCC 影响费率**：不同 MCC 类目对应不同的手续费费率，校验费率计算时需关注 mcc。
2. **merchant_id ≠ partner_id**：partner_id 是一级商户，merchant_id 是二级商户，勿混用。
3. **聚合支付场景才有**：非聚合订单 `t_secondary_merchant_detail` 可能为空，需区分订单类型再校验。
4. **风控关注 MCC**：高风险 MCC（如赌博、成人）会被严格风控，需覆盖此类用例。
5. 与 `t_acquire_order` 通过 `global_id` 1:1 关联，校验数据一致性。
