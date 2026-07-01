---
id: tbl_member_tm_member
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
- member-profile
- tm_member
subdomain: member-profile
module: null
sensitivity: normal
name: 会员信息表(tm_member)
aliases:
- tm_member
related_services:
- svc_member
related_scenarios: []
---

# 会员信息表(tm_member)

## 用途
会员信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `MEMBER_ID` | varchar(32) | PK / NOT NULL | 会员ID |
| `MEMBER_NAME` | varchar(255) |  | 会员名称 |
| `MEMBER_SHORT_NAME` | varchar(60) |  | 会员缩略名,已注销的会被添加后缀 |
| `MEMBER_TYPE` | decimal(8) | NOT NULL | 会员类型(1个人 2 公司 3 组织) |
| `STATUS` | decimal(8) | NOT NULL | 会员状态(0未激活 1正常 2休眠 3注销) |
| `LOCK_STATUS` | decimal(8) | NOT NULL | 会员锁定状态(0未锁定 1已锁定) |
| `FROM_IP` | varchar(30) |  | IP地址 |
| `ACTIVE_TIME` | timestamp |  | 激活时间 |
| `CREATE_TIME` | timestamp |  | 建立时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `MEMO` | varchar(255) |  | 备注信息 |
| `SOURCE_ID` | varchar(128) |  | 注册来源ID |
| `CPS_TYPE` | varchar(50) |  | 风控用户类型 |
| `SUB_LEVEL` | varchar(128) |  | vip子等级 |
| `OWNER_ID` | varchar(128) |  | 归属ID |

## 主键 / 索引
- 主键:(`MEMBER_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
