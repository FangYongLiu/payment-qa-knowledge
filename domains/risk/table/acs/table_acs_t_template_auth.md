---
id: tbl_acs_t_template_auth
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
- t_template_auth
subdomain: acs
module: null
sensitivity: normal
name: 接口授权模版(t_template_auth)
aliases:
- t_template_auth
related_services:
- svc_acs
related_scenarios: []
---
# 接口授权模版(t_template_auth)

## 用途
接口授权模版。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `TEMPLATE_AUTH_ID` | decimal(8) | PK / NOT NULL | 接口授权模版ID |
| `API_ID` | decimal(8) | NOT NULL | API接口ID |
| `OUTER_CODE` | varchar(64) |  | 外部业务码 |
| `TEMPLATE_ACCOUNT_ID` | decimal(8) |  | 授权账户模版ID |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFY` | timestamp | NOT NULL | 修改时间 |
| `MEMO` | varchar(256) |  | 备注 |

## 主键 / 索引
- 主键:(`TEMPLATE_AUTH_ID`)
- 唯一约束:
  - `UK_T_TEMPLATE_AUTH` 唯一 (API_ID, OUTER_CODE, TEMPLATE_ACCOUNT_ID)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
