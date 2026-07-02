---
id: tbl_bps_t_payroll_card
object_type: Table
name: payby工资卡表 (t_payroll_card)
aliases: [t_payroll_card, bps.t_payroll_card]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bps schema DDL
tags: [wps, bps]
sensitivity: normal
related_services: []
---

# payby工资卡表 (t_payroll_card)

## 用途
物理表 `bps.t_payroll_card`,主键 `id`。payby工资卡表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `cardholder_employee_id` | char(32) | 持卡人 |
| `cardholder_wallet_id` | varchar(32) | payby钱包id |
| `card_applied_corporate_id` | char(32) | 下发公司id |
| `current_employer_corporate_id` | char(32) | 当前公司id |
| `name_on_card` | varchar(26) | 卡名 |
| `fourth_line_emboss_name` | char(10) | 第四个名称 · 可空 |
| `proxy_number` | varchar(32) | 代号 · 可空 |
| `card_number` | varchar(32) | 卡号 · 可空 |
| `delivery_status` | varchar(16) | 下发状态 |
| `tenant_code` | varchar(32) | 商户号 |
| `status` | varchar(20) | 员工状态 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
