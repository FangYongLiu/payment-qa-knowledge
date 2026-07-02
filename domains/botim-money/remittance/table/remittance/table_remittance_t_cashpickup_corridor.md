---
id: tbl_remittance_t_cashpickup_corridor
object_type: Table
name: Cash pickup corridor config (pickup days + map locator) (t_cashpickup_corridor)
aliases: [t_cashpickup_corridor, remittance.t_cashpickup_corridor]
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

# Cash pickup corridor config (pickup days + map locator) (t_cashpickup_corridor)

## 用途
物理表 `remittance.t_cashpickup_corridor`,主键 `id`。Cash pickup corridor config (pickup days + map locator)。业务语义细节**待补**(表结构来自 DDL)。

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
| `max_pickup_days` | int | Max days cash can be picked up; NULL = no limit / not configured · 可空 |
| `enable_flag` | char | Enable flag: Y/N |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- `uk_cashpickup_corridor`:channel_code, country_code, currency (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
