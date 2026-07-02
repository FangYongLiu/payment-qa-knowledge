---
id: tbl_protocol_t_contract_day_statistics
object_type: Table
name: t_contract_day_statistics (t_contract_day_statistics)
aliases: [t_contract_day_statistics, protocol.t_contract_day_statistics]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: protocol schema DDL
tags: [wallet, protocol]
sensitivity: normal
related_services: []
---

# t_contract_day_statistics (t_contract_day_statistics)

## 用途
物理表 `protocol.t_contract_day_statistics`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键id · 可空 |
| `contract_type` | varchar(25) | 协议类型 |
| `contract_sub_type` | varchar(32) | 协议子类型 |
| `statistics_type` | varchar(32) | 定义统计字段 |
| `dimension_hash` | varchar(64) | 统计维度 |
| `statistics_field` | varchar(128) | 统计字段字符串 |
| `quantity` | int | 签约数 |
| `statistics_day` | varchar(12) | 日期 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
