---
id: tbl_transfer_t_split_bill_share_record
object_type: Table
name: 账单分享记录 (t_split_bill_share_record)
aliases: [t_split_bill_share_record, transfer.t_split_bill_share_record]
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

# 账单分享记录 (t_split_bill_share_record)

## 用途
物理表 `transfer.t_split_bill_share_record`,主键 `share_id`。账单分享记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `share_id` | bigint | 分享ID |
| `bill_no` | bigint | 账单编号 |
| `type` | varchar(10) | 类型(MSG:短信、LINK:链接,FRIEND:好友) |
| `content` | varchar(150) | 内容 · 可空 |
| `receiver_mid` | varchar(32) | 接收人mid · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `sub_bill_no` | bigint | 子账单编号 · 可空 |
| `send_mode` | varchar(10) | 类型(MSG:短信、AO:公众号) |
| `receiver_uid` | varchar(32) | 接收人uid · 可空 |
| `receiver_pid` | varchar(32) | 接收人pid · 可空 |
| `receiver_mobile` | varchar(32) | 接收人手机号 · 可空 |

## 主键 / 索引
- 主键:`share_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
