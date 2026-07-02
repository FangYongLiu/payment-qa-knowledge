---
id: tbl_transfer_t_redpkg_protocol
object_type: Table
name: 加密Key唯一 (t_redpkg_protocol)
aliases: [t_redpkg_protocol, transfer.t_redpkg_protocol]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: transfer schema DDL
tags: [wallet, transfer]
sensitivity: normal
related_services: []
---

# 加密Key唯一 (t_redpkg_protocol)

## 用途
物理表 `transfer.t_redpkg_protocol`,主键 `id`。加密Key唯一。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 主键 |
| `encrypt_key` | varchar(32) | 加密Key |
| `payment_no` | bigint(18) | 支付订单号 |
| `url` | varchar(200) | 短链接 |
| `value` | varchar(500) | JSON格式的参数字段 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
