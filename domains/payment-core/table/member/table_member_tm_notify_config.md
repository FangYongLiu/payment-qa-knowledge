---
id: tbl_member_tm_notify_config
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- notify
- tm_notify_config
subdomain: notify
module: null
sensitivity: normal
name: Notify config(tm_notify_config)
aliases:
- tm_notify_config
related_services:
- svc_member
related_scenarios: []
---

# Notify config(tm_notify_config)

## 用途
Notify config。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `config_id` | int | PK | Config id |
| `biz_type` | varchar(30) | NOT NULL | Business type;MER_PORTAL_LOGIN_PWD |
| `method` | varchar(15) |  | Notify method;SMS,MAIL |
| `subject` | varchar(100) |  | Notify subject |
| `template_id` | varchar(50) |  | Notify content |
| `notify_rules` | varchar(70) |  | Notify rules |
| `retry_rules` | varchar(50) |  | Retry rules |
| `enable_flag` | char | NOT NULL / 默认 'Y' | Enable flag;Y,N |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`config_id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
