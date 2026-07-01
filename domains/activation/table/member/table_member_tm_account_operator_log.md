---
id: tbl_member_tm_account_operator_log
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
- tm_account_operator_log
subdomain: operator-security
module: null
sensitivity: normal
name: 账户操作记录表(tm_account_operator_log)
aliases:
- tm_account_operator_log
related_services:
- svc_member
related_scenarios: []
---

# 账户操作记录表(tm_account_operator_log)

## 用途
账户操作记录表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(32) | PK / NOT NULL | 主键 |
| `member_id` | varchar(20) | NOT NULL | 会员编号 |
| `type` | varchar(32) | NOT NULL | 账户类型 |
| `freeze_status` | char |  | 账户状态类型，0:未冻结  1:止出  2:止入 3:双向冻结(锁定) |
| `status` | char | NOT NULL | 状态 S ：处理成功， F: 处理失败， I: 无效 |
| `biz_source` | varchar(32) |  | 业务来源 |
| `client_id` | varchar(55) |  | 应用ID |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |
| `memo` | varchar(255) |  | 备注 |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
