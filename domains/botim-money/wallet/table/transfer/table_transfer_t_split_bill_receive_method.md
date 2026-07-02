---
id: tbl_transfer_t_split_bill_receive_method
object_type: Table
name: 分账收款方式 (t_split_bill_receive_method)
aliases: [t_split_bill_receive_method, transfer.t_split_bill_receive_method]
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

# 分账收款方式 (t_split_bill_receive_method)

## 用途
物理表 `transfer.t_split_bill_receive_method`,主键 `id`。分账收款方式。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 |
| `bill_no` | bigint | 账单编号 |
| `receive_method` | varchar(15) | 收款方式 |
| `link` | varchar(200) | 短链 |
| `memo` | varchar(200) | 备注 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
