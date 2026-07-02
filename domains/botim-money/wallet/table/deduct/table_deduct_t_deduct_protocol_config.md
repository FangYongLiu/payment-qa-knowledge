---
id: tbl_deduct_t_deduct_protocol_config
object_type: Table
name: Deduct Protocol Config (t_deduct_protocol_config)
aliases: [t_deduct_protocol_config, deduct.t_deduct_protocol_config]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: deduct schema DDL
tags: [wallet, deduct]
sensitivity: normal
related_services: []
---

# Deduct Protocol Config (t_deduct_protocol_config)

## 用途
物理表 `deduct.t_deduct_protocol_config`,主键 `id`。Deduct Protocol Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID · 可空 |
| `protocol_scene_code` | char(3) | Protocol Scene Code |
| `deduct_type` | char(2) | Deduct Type;SP=Special Pay Method, LP=Loop Pay Method |
| `protocol_type` | varchar(20) | Protocol Type |
| `protocol_sub_type` | varchar(30) | Protocol Sub Type |
| `period` | char (4) | Protocol period. Y=Year, M=Month, D=Day |
| `partner_id` | varchar(255) | Allowed partner id;ALL=All partner id, multi split by comma(,) |
| `merchant_id` | varchar(255) | Allowed merchant id;ALL=All merchant id, multi split by comma(,) |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |
| `protocol_party` | char | Protocol Party; B=Bilateral, T=Tripartite |

## 主键 / 索引
- 主键:`id`
- `uk_protocol_scene_code`:protocol_scene_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
