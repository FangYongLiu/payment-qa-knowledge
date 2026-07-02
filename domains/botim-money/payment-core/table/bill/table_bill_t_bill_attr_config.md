---
id: tbl_bill_t_bill_attr_config
object_type: Table
name: 账单属性配置表 (t_bill_attr_config)
aliases: [t_bill_attr_config, bill.t_bill_attr_config]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bill schema DDL
tags: [payment-core, bill]
sensitivity: normal
related_services: []
---

# 账单属性配置表 (t_bill_attr_config)

## 用途
物理表 `bill.t_bill_attr_config`,主键 `id`。账单属性配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 业务ID · 可空 |
| `biz_product_code` | varchar(32) | 业务产品码 |
| `role` | varchar(32) | 角色 |
| `payment_type` | varchar(32) | 支付方式(pay,refund,revert) |
| `status` | varchar(32) | 状态码 |
| `attr_code` | varchar(32) | 属性编码 |
| `attr_value` | varchar(32) | 属性值 |
| `attr_value_type` | varchar(32) | 待补 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_pc_role_pt_st_attr`:biz_product_code, role, payment_type, status, attr_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
