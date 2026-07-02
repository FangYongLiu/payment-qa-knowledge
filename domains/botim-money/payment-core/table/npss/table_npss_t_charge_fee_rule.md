---
id: tbl_npss_t_charge_fee_rule
object_type: Table
name: 收费策略 (t_charge_fee_rule)
aliases: [t_charge_fee_rule, npss.t_charge_fee_rule]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# 收费策略 (t_charge_fee_rule)

## 用途
物理表 `npss.t_charge_fee_rule`,主键 `fee_id`。收费策略。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `fee_id` | int | id · 可空 |
| `biz_product_code` | char(6) | 业务产品码 |
| `platform` | char(5) | 平台,payby/aani · 可空 |
| `charge_bearer` | char(5) | 收费方, payer-付款方收费，payee-收款方收费 |
| `fix_charge` | decimal(10, 4) | 手续费规则，单笔固定费用，单位aed · 可空 |
| `percent_charge` | decimal(10, 4) | 手续费规则，百分比费用，需要除以100 · 可空 |
| `memo` | varchar(256) | 备注 · 可空 |
| `enable` | char | 状态: Y-可用，N-不可用 · 可空 |
| `gmt_effect` | timestamp | 生效时间 · 可空 |
| `gmt_expired` | timestamp | 失效时间 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`fee_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
