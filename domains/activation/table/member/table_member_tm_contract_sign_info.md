---
id: tbl_member_tm_contract_sign_info
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
- tm_contract_sign_info
subdomain: contract
module: null
sensitivity: normal
name: 协议签署信息(tm_contract_sign_info)
aliases:
- tm_contract_sign_info
related_services:
- svc_member
related_scenarios: []
---

# 协议签署信息(tm_contract_sign_info)

## 用途
协议签署信息。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `SIGN_ID` | decimal(17) | PK / NOT NULL | 签署ID |
| `user_id` | varchar(50) | NOT NULL | 用户ID |
| `PARTNER_ID` | varchar(32) | NOT NULL | 商户ID |
| `CONTRACT_TYPE` | varchar(32) | NOT NULL | 协议类型 |
| `CONTRACT_NAME` | varchar(512) | NOT NULL |  |
| `SIGN_TIME` | timestamp | NOT NULL | 签署时间 |
| `RELIEVE_TIME` | timestamp |  | 解约时间 |
| `EXTENSION` | varchar(512) |  | 扩展字段 |
| `STATUS` | char | NOT NULL | 状态 Y 有效 / N 无效 |
| `MEMO` | varchar(512) |  | 备注 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp | NOT NULL | 修改时间 |
| `version` | varchar(50) |  | verion |
| `address` | varchar(150) |  | 协议地址 |

## 主键 / 索引
- 主键:(`SIGN_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
