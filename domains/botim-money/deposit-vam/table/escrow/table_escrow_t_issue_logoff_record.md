---
id: tbl_escrow_t_issue_logoff_record
object_type: Table
name: 注销信息 唯一索引 (t_issue_logoff_record)
aliases: [t_issue_logoff_record, escrow.t_issue_logoff_record]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 注销信息 唯一索引 (t_issue_logoff_record)

## 用途
物理表 `escrow.t_issue_logoff_record`,主键 `id`。注销信息 唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | id |
| `card_no` | varchar(32) | 银行卡编号 |
| `card_id` | varchar(32) | 银行卡ID |
| `id_num` | varchar(32) | 身份证号 · 可空 |
| `member_id` | varchar(32) | 会员编号 |
| `bank_code` | varchar(8) | 银行编号 |
| `client_id` | varchar(32) | clientId，客户端标识 |
| `status` | varchar(4) | 注销状态，S-Success注销成功，F-Fail注销失败，P-Processing处理中，A-AWAIT待处理 |
| `logoff_type` | varchar(32) | 注销类型 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 更新时间 · 可空 |
| `gmt_report` | timestamp | 如果需要注销虚拟卡信息，记录上报时间 · 可空 |
| `memo` | varchar(512) | memo · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
