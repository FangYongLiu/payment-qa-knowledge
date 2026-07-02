---
id: tbl_ccctron_t_signed_transaction
object_type: Table
name: 签名交易 (t_signed_transaction)
aliases: [t_signed_transaction, ccctron.t_signed_transaction]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccctron schema DDL
tags: [crypto, ccctron]
sensitivity: normal
related_services: []
---

# 签名交易 (t_signed_transaction)

## 用途
物理表 `ccctron.t_signed_transaction`,主键 `id`。签名交易。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(100) | id |
| `body` | varchar(2000) | 报文base64 |
| `created_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
