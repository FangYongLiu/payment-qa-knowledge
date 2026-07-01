---
id: tbl_acs_t_withhold_auth_log
object_type: Table
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (acs schema) 2026-06-25
tags:
- acs
- acs
- t_withhold_auth_log
subdomain: acs
module: null
sensitivity: normal
name: 委托代扣操作日志(t_withhold_auth_log)
aliases:
- t_withhold_auth_log
related_services:
- svc_acs
related_scenarios: []
---
# 委托代扣操作日志(t_withhold_auth_log)

## 用途
委托代扣操作日志。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(17) | PK / NOT NULL | 主键 ID |
| `WITHHOLD_AUTH_ID` | decimal(8) | NOT NULL | 委托代扣 ID |
| `TYPE` | char | NOT NULL | 操作类型:O -- open,开通;C -- close,关闭 |
| `EXT` | varchar(512) |  | 扩展参数 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:
  - `I_WITHHOLD_AUTH_LOG_CREATETIME` (CREATE_TIME)
  - `I_WITHHOLD_AUTH_LOG_WITHHOLDID` (WITHHOLD_AUTH_ID)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
