---
id: tbl_basiscustomer_t_prepaid_audit_config
object_type: Table
name: 预付费审核配置表 (t_prepaid_audit_config)
aliases: [t_prepaid_audit_config, basiscustomer.t_prepaid_audit_config]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basiscustomer schema DDL
tags: [activation, basiscustomer]
sensitivity: normal
related_services: []
---

# 预付费审核配置表 (t_prepaid_audit_config)

## 用途
物理表 `basiscustomer.t_prepaid_audit_config`,主键 `id`。预付费审核配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `currency` | char(3) | 币种 |
| `sell_cost_max_limit` | decimal(19, 4) | 卖出成本最高限制 |
| `sell_cost_min_limit` | decimal(19, 4) | 卖出成本最低限制 |
| `buy_cost_max_limit` | decimal(19, 4) | 买入成本最高限制 |
| `buy_cost_min_limit` | decimal(19, 4) | 买入成本最低限制 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_currency`:currency (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
