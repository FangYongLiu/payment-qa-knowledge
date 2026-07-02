---
id: tbl_bps_t_employee_kyc_material
object_type: Table
name: kyc材料表 (t_employee_kyc_material)
aliases: [t_employee_kyc_material, bps.t_employee_kyc_material]
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

# kyc材料表 (t_employee_kyc_material)

## 用途
物理表 `bps.t_employee_kyc_material`,主键 `id`。kyc材料表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `employee_id` | varchar(64) | 员工表主键 |
| `employee_registration_id` | varchar(100) | 员工MOL ID |
| `corporate_registration_id` | varchar(64) | 公司MOL ID |
| `employee_number` | varchar(64) | 员工No |
| `corporate_number` | varchar(64) | 公司No |
| `material_type` | varchar(16) | 材料类型 |
| `kyc_identity` | varchar(64) | eid或password · 可空 |
| `ufs_file` | varchar(256) | 材料地址 |
| `status` | varchar(16) | 状态 |
| `tenant_code` | varchar(32) | 商户号 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
