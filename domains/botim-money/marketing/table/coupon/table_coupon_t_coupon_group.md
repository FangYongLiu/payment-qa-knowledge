---
id: tbl_coupon_t_coupon_group
object_type: Table
name: t_coupon_group (t_coupon_group)
aliases: [t_coupon_group, coupon.t_coupon_group]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: coupon schema DDL
tags: [marketing, coupon]
sensitivity: normal
related_services: []
---

# t_coupon_group (t_coupon_group)

## 用途
物理表 `coupon.t_coupon_group`,主键 `group_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `group_id` | int(12) | 主键 · 可空 |
| `group_name` | varchar(32) | 优惠券组名称 · 可空 |
| `desc` | varchar(255) | 描述 · 可空 |
| `status` | tinyint(2) | 1:有效；0:无效 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`group_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
