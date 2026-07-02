---
id: tbl_bps_t_employee_salary_account
object_type: Table
name: 员工工资账户表 (t_employee_salary_account)
aliases: [t_employee_salary_account, bps.t_employee_salary_account]
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

# 员工工资账户表 (t_employee_salary_account)

## 用途
物理表 `bps.t_employee_salary_account`,主键 `id`。员工工资账户表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `salary_account_type` | char(10) | 工资账户类型 |
| `wallet_id` | varchar(32) | payby钱包id · 可空 |
| `card_ref_mid` | varchar(32) | 卡关联的钱包id · 可空 |
| `card_ref_vid` | varchar(32) | 卡关联的虚拟id · 可空 |
| `salary_loading_IBAN` | varchar(32) | payby IBAN · 可空 |
| `routing_code` | varchar(32) | 路由编号 |
| `card_type` | varchar(26) | card type · 可空 |
| `tenant_code` | varchar(32) | 商户号 |
| `data_version` | bigint | 版本号 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
