---
id: tbl_member_td_config
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
- td_config
subdomain: config
module: null
sensitivity: normal
name: 配置表(td_config)
aliases:
- td_config
related_services:
- svc_member
related_scenarios: []
---

# 配置表(td_config)

## 用途
配置表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | bigint | PK | 配置ID |
| `TYPE` | varchar(50) | NOT NULL | 配置类型 |
| `SUB_TYPE` | varchar(50) | NOT NULL | 配置子类型 |
| `VALUE` | varchar(255) | NOT NULL | 配置值 |
| `STATUS` | decimal(8) | NOT NULL | 状态(0不可用 1可用) |
| `TYPE_DESC` | varchar(255) |  | 类型描述 |
| `VALUE_DESC` | varchar(255) |  | 值描述 |
| `ORDER_NO` | decimal(8) |  | 顺序号 |
| `CREATE_TIME` | timestamp |  | 建立时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `CREATE_USER` | varchar(50) |  | 建立人 |
| `UPDATE_USER` | varchar(50) |  | 更新人 |
| `MEMO` | varchar(255) |  | 备注信息 |
| `EXT1` | varchar(255) |  | 扩展字段1 |
| `EXT2` | varchar(255) |  | 扩展字段2 |
| `EXT3` | varchar(255) |  | 扩展字段3 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
