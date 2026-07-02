---
id: tbl_cashierii_t_business_scene
object_type: Table
name: 业务场景 (t_business_scene)
aliases: [t_business_scene, cashierii.t_business_scene]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cashierii schema DDL
tags: [payment-core, cashierii]
sensitivity: normal
related_services: []
---

# 业务场景 (t_business_scene)

## 用途
物理表 `cashierii.t_business_scene`,主键 `id`。业务场景。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | ID · 可空 |
| `scene_code` | varchar(20) | Scene Code |
| `pay_scene` | varchar(20) | Pay Scene |
| `biz_product_code` | char(6) | Biz Product Code |
| `memo` | varchar(64) | Memo · 可空 |
| `create_time` | timestamp(3) | Create Time |
| `update_time` | timestamp(3) | Update Time |

## 主键 / 索引
- 主键:`id`
- `uk_code_and_pay_scene`:scene_code, pay_scene (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
