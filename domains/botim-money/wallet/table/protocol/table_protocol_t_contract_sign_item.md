---
id: tbl_protocol_t_contract_sign_item
object_type: Table
name: 签署协议条款表 (t_contract_sign_item)
aliases: [t_contract_sign_item, protocol.t_contract_sign_item]
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

# 签署协议条款表 (t_contract_sign_item)

## 用途
物理表 `protocol.t_contract_sign_item`,主键 `id`。签署协议条款表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `sign_info_id` | bigint(25) | 协议ID |
| `enabled` | varchar(8) | 状态（Y：有效，N：无效） |
| `contract_item` | varchar(1024) | 签约的条款内容，json格式数据 · 可空 |
| `contract_desc` | varchar(255) | 条款内容描述 · 可空 |
| `biz_id` | varchar(50) | 业务ID · 可空 |
| `biz_type` | varchar(35) | 业务类型 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `idx_biz_id_type`:biz_id, biz_type
- `idx_sign_info_id`:sign_info_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
