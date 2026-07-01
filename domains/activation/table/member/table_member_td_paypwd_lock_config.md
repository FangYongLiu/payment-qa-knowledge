---
id: tbl_member_td_paypwd_lock_config
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
- password-security
- td_paypwd_lock_config
subdomain: password-security
module: null
sensitivity: normal
name: 支付密码锁定配置表(td_paypwd_lock_config)
aliases:
- td_paypwd_lock_config
related_services:
- svc_member
related_scenarios: []
---

# 支付密码锁定配置表(td_paypwd_lock_config)

## 用途
支付密码锁定配置表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | bigint | PK | 配置ID |
| `LOCK_STRATEGY` | varchar(30) | NOT NULL | 锁定策略 |
| `INPUT_DETECT_SPAN` | decimal(8) | NOT NULL | 错误输入检测时间段(以分钟记) |
| `WRONG_INPUT_COUNT` | decimal(8) | NOT NULL | 触发锁定的错误输入次数 |
| `LOCK_SPAN` | decimal(8) | NOT NULL | 锁定时间段(以分钟记) |
| `STATUS` | decimal(8) |  | 状态(0不可用;1可用) |
| `MEMO` | varchar(255) |  | 备注 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
