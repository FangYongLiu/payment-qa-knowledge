---
id: tbl_member_tm_contract_sign_log
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
- contract
- tm_contract_sign_log
subdomain: contract
module: null
sensitivity: normal
name: 协议签署历史记录(tm_contract_sign_log)
aliases:
- tm_contract_sign_log
related_services:
- svc_member
related_scenarios: []
---

# 协议签署历史记录(tm_contract_sign_log)

## 用途
协议签署历史记录。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `LOG_ID` | decimal(17) | PK / NOT NULL | 记录ID |
| `SIGN_ID` | decimal(17) | NOT NULL | 签署ID |
| `CONTRACT_NAME` | varchar(512) | NOT NULL | 协议名称 |
| `OPERATE_TYPE` | char | NOT NULL | 操作类型 S 签约 R 解除签约 |
| `EXTENSION` | varchar(512) |  | 扩展字段 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`LOG_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
