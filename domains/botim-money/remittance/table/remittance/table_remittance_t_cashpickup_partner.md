---
id: tbl_remittance_t_cashpickup_partner
object_type: Table
name: Cash pickup payout partner/brand list (t_cashpickup_partner)
aliases: [t_cashpickup_partner, remittance.t_cashpickup_partner]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: remittance schema DDL
tags: [remittance, remittance]
sensitivity: normal
related_services: []
---

# Cash pickup payout partner/brand list (t_cashpickup_partner)

## 用途
物理表 `remittance.t_cashpickup_partner`,主键 `id`。Cash pickup payout partner/brand list。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `channel_code` | varchar(32) | Channel code: MG,IME,BDO,TB,MC |
| `country_code` | varchar(10) | Receiving country code |
| `currency` | varchar(3) | Payout currency |
| `partner_code` | varchar(32) | Payout partner/brand code |
| `partner_name` | varchar(128) | Payout partner/brand name (A-Z display) |
| `icon` | varchar(255) | Brand icon URL · 可空 |
| `sort_no` | int | Sort order; defaults to name A-Z · 可空 |
| `enable_flag` | char | Enable flag: Y/N |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- `uk_cashpickup_partner`:channel_code, country_code, currency, partner_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
