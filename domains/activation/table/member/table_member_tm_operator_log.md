---
id: tbl_member_tm_operator_log
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
- operator-security
- tm_operator_log
subdomain: operator-security
module: null
sensitivity: normal
name: 会员操作记录表(tm_operator_log)
aliases:
- tm_operator_log
related_services:
- svc_member
related_scenarios: []
---

# 会员操作记录表(tm_operator_log)

## 用途
会员操作记录表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `OP_LOG_ID` | bigint(32) | PK / NOT NULL | 主键 |
| `MEMBER_ID` | varchar(32) |  | 会员编号 |
| `IDENTITY` | varchar(32) |  | 标识 |
| `CLIENT_ID` | varchar(32) | NOT NULL | 请求系统编号 |
| `OP_TYPE` | varchar(32) |  | 操作类型 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `UPDATE_TIME` | timestamp |  | 订单更新时间 |
| `OP_STATUS` | varchar(32) |  | 拓展信息 |
| `MESSAGE` | varchar(155) |  | Message |
| `OPERATOR_NAME` | varchar(55) |  | Operator name |
| `MEMO` | varchar(255) |  | 备注 |

## 主键 / 索引
- 主键:(`OP_LOG_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
