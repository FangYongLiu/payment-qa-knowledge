---
id: tbl_onboarding_t_open_product_package_order
object_type: Table
name: open_product_package_order (t_open_product_package_order)
aliases: [t_open_product_package_order, onboarding.t_open_product_package_order]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: onboarding schema DDL
tags: [merchant-management, onboarding]
sensitivity: normal
related_services: []
---

# open_product_package_order (t_open_product_package_order)

## 用途
物理表 `onboarding.t_open_product_package_order`,主键 `id`。open_product_package_order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `product_package_code` | varchar(50) | product_package_code |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
