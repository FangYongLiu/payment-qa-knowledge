---
id: tbl_member_tr_member_ext_info
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
- member-profile
- tr_member_ext_info
subdomain: member-profile
module: null
sensitivity: normal
name: 会员扩展信息表(tr_member_ext_info)
aliases:
- tr_member_ext_info
related_services:
- svc_member
related_scenarios: []
---

# 会员扩展信息表(tr_member_ext_info)

## 用途
会员扩展信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `EXT_ID` | decimal(28) | PK / NOT NULL | 主键 |
| `MEMBER_ID` | varchar(32) | NOT NULL | 会员ID |
| `PROP_KEY` | varchar(20) | NOT NULL | 属性键 |
| `PROP_VALUE` | varchar(1024) |  | 属性值 |
| `STATUS` | decimal(8) |  | 状态(0不可用 1可用) |
| `CREATE_TIME` | timestamp |  | 建立时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `MEMO` | varchar(255) |  | 备注信息 |

## 主键 / 索引
- 主键:(`EXT_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
