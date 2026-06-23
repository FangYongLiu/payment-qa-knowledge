---
id: tbl_transferii_t_order_permit
object_type: Table
domain: fund-out-transfer
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:654d5bef-1e1a-485d-a44b-c83918b7165b
tags:
- transferii
- collect-permit
subdomain: wallet-order
module: null
sensitivity: normal
name: 订单收款凭证表 t_order_permit
aliases:
- t_order_permit
- Collect Permit
related_services: []
related_tables:
- tbl_transferii_t_wallet_order
- tbl_transferii_t_party_order
- tbl_transferii_t_cancel_order
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
`transferii.t_order_permit` 用于存放钱包订单的 Collect Permit(收款许可凭证)。每条记录通过 `wallet_order_no` 关联到主表 `t_wallet_order`，标识收款方可以凭何种凭证(如手机号、邮箱等)来领取/收款该笔钱包订单的资金。

## 关键列
| 列名 | 含义 | Key | 类型 | 长度 |
|---|---|---|---|---|
| permit_id | Permit ID | PK | bigint | - |
| wallet_order_no | Wallet Order No(关联钱包订单) | FK | bigint | - |
| permit_type | Permit Type(凭证类型) | - | char | 1 |
| permit_value | Permit Value(凭证值) | - | varchar | 32 |

## 主键/索引
- 主键：`permit_id`
- 外键：`wallet_order_no` → `t_wallet_order.wallet_order_no`

## 校验点(QA 关注)
- `wallet_order_no` 必须存在于 `t_wallet_order` 中；外键完整性。
- `permit_type` 为 char(1)：需校验取值集合是否被业务白名单约束(原文未列举具体编码，测试时需对照实际枚举)。
- `permit_value` 长度上限 32：超长输入应被拒绝；不同 `permit_type` 对应的 `permit_value` 格式(如手机号、邮箱)需符合各自业务校验规则。
- 注意 `t_wallet_order.wallet_order_no` 在主表为 varchar(32)，而本表 `wallet_order_no` 标注为 bigint —— 类型不一致是潜在数据质量/JOIN 风险点，QA 应重点确认 schema 与实际实现是否对齐。
- 一个 `wallet_order_no` 可能对应多条 permit 记录(多凭证场景)，需验证唯一性约束与重复插入处理。
