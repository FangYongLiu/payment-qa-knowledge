---
id: tbl_commission_t_common_config_version
object_type: Table
name: DCC Rebate Common Config Version (t_common_config_version)
aliases: [t_common_config_version, commission.t_common_config_version]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: commission schema DDL
tags: [settlement, commission]
sensitivity: normal
related_services: []
---

# DCC Rebate Common Config Version (t_common_config_version)

## 用途
物理表 `commission.t_common_config_version`,主键 `version_id`。DCC Rebate Common Config Version。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `version_id` | bigint | Config Version Id · 可空 |
| `comm_config_id` | bigint | Commission Config Id |
| `rebate_rate` | decimal(10, 6) | Rebate Rate |
| `operator` | varchar(50) | Operator · 可空 |
| `extension` | varchar(255) | Extension Field · 可空 |
| `create_time` | timestamp | Creation Time |

## 主键 / 索引
- 主键:`version_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
