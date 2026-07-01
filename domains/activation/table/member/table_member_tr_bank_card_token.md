---
id: tbl_member_tr_bank_card_token
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
- card-binding
- tr_bank_card_token
subdomain: card-binding
module: null
sensitivity: normal
name: 银行卡渠道信息(tr_bank_card_token)
aliases:
- tr_bank_card_token
related_services:
- svc_member
related_scenarios: []
---

# 银行卡渠道信息(tr_bank_card_token)

## 用途
银行卡渠道信息。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `token_id` | int | PK / NOT NULL | 主键id |
| `card_id` | int | NOT NULL | 卡ID |
| `institution_code` | varchar(32) |  | 机构编号 |
| `token` | varchar(64) | NOT NULL | 银行渠道返回的唯一TOKEN |
| `channel` | varchar(32) | NOT NULL | 银行渠道编号 |
| `status` | char |  | 状态：Y/N |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`token_id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
