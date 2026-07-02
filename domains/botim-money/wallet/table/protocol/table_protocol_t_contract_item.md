---
id: tbl_protocol_t_contract_item
object_type: Table
name: 协议条款表 (t_contract_item)
aliases: [t_contract_item, protocol.t_contract_item]
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

# 协议条款表 (t_contract_item)

## 用途
物理表 `protocol.t_contract_item`,主键 `id`。协议条款表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `template_id` | bigint(25) | 模版id |
| `item_type` | varchar(35) | 条款类型  如：费率条款，支付条款，结算条款 |
| `item_desc` | varchar(25) | 条款类型描述 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `memo` | varchar(255) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
