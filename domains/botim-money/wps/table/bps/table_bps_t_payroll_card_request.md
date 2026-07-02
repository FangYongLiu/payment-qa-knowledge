---
id: tbl_bps_t_payroll_card_request
object_type: Table
name: payby工资卡请求表 (t_payroll_card_request)
aliases: [t_payroll_card_request, bps.t_payroll_card_request]
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

# payby工资卡请求表 (t_payroll_card_request)

## 用途
物理表 `bps.t_payroll_card_request`,主键 `id`。payby工资卡请求表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `employee_id` | char(32) | 员工id |
| `customer_number` | char(10) | 员工编号 |
| `product_code` | varchar(32) | 产品编号 |
| `routing_code` | varchar(32) | 路由编号 |
| `name_on_card` | varchar(26) | 卡名 · 可空 |
| `fourth_line_emboss_name` | char(10) | 第四个名称 · 可空 |
| `tenant_code` | varchar(32) | 商户号 |
| `status` | varchar(20) | 请求状态 |
| `memo` | varchar(100) | 备注 · 可空 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
