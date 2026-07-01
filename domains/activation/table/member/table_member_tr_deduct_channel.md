---
id: tbl_member_tr_deduct_channel
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
- tr_deduct_channel
subdomain: card-binding
module: null
sensitivity: restricted
name: 扣款渠道表(tr_deduct_channel)
aliases:
- tr_deduct_channel
related_services:
- svc_member
related_scenarios: []
---

# 扣款渠道表(tr_deduct_channel)

## 用途
扣款渠道表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | int(10) | PK | 主键 |
| `MEMBER_ID` | varchar(32) | NOT NULL / 默认 '' | 会员id |
| `ACCOUNT_TOKEN` | varchar(32) | 默认 '' | 账号标记 |
| `ACCOUNT_NO` | varchar(32) | 默认 '' | 渠道值 |
| `ACCOUNT_TYPE` | varchar(16) | 默认 '' | 渠道类型（CARD 银行卡 BALANCE 余额） |
| `PAY_CHANNEL` | varchar(10) | 默认 '' | 14-余额 15-快捷 |
| `QUOTA` | decimal(15,2) |  | 支付限额 |
| `STATUS` | varchar(3) | 默认 '' | 状态（1有效   0无效） |
| `CREATE_TIME` | timestamp |  | 创建时间 |
| `MODIFY_TIME` | timestamp |  | 修改时间 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
