---
id: tbl_remittance_t_member_relationship
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_member_relationship
subdomain: remittance
module: null
sensitivity: normal
name: 会员关系表(t_member_relationship)
aliases:
- t_member_relationship
related_services:
- svc_remittance
related_scenarios: []
---
# 会员关系表(t_member_relationship)

## 用途
会员关系表。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `member_id` | varchar(20) | NOT NULL | 会员id |
| `partner_id` | varchar(20) |  | 来源平台 |
| `channel_code` | varchar(10) |  | 渠道号 |
| `channel_member_id` | varchar(32) |  | 渠道会员标示 |
| `eid_card_no` | varchar(32) |  | eid 卡号 |
| `status` | char(4) |  | 状态: AS - 激活,AF - 激活失败,NA - 未激活,NK - 未KYC,EK - KYC过期 |
| `activate_time` | timestamp |  | 激活时间 |
| `apply_counting` | int | 默认 0 | 汇款次数 |
| `success_counting` | int | 默认 0 | 汇款成功次数 |
| `last_pay_time` | timestamp |  | 最后付款时间 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |
| `extension` | varchar(255) |  | 扩展参数 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_mid` (member_id)
  - `idx_update_time` (update_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
