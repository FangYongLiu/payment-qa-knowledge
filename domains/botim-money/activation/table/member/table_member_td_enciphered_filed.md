---
id: tbl_member_td_enciphered_filed
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- config
- td_enciphered_filed
subdomain: config
module: null
sensitivity: normal
name: 加密数据字典(td_enciphered_filed)
aliases:
- td_enciphered_filed
related_services:
- svc_member
related_scenarios: []
---

# 加密数据字典(td_enciphered_filed)

## 用途
加密数据字典。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `FILED_ID` | bigint | PK | 配置ID |
| `COLUMN_NAME` | varchar(32) | NOT NULL | 列名 |
| `ENCIPHERED_TYPE` | varchar(10) | NOT NULL | 加密方式 UES |
| `SUMMARY_RULE` | varchar(512) |  | 摘要规则 |
| `CREATE_DATE` | timestamp |  | 建立时间 |
| `UPDATE_DATE` | timestamp |  | 更新时间 |
| `MEMO` | varchar(256) |  | 创建人 |
| `TICKET_SUMMARY_RULE` | varchar(512) |  | ticket备注规则 |

## 主键 / 索引
- 主键:(`FILED_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
