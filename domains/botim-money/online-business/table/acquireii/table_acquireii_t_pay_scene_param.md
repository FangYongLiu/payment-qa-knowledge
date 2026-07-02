---
id: tbl_acquireii_t_pay_scene_param
object_type: Table
name: 支付场景参数 (t_pay_scene_param)
aliases: [t_pay_scene_param, acquireii.t_pay_scene_param]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquireii schema DDL
tags: [online-business, acquireii]
sensitivity: normal
related_services: []
---

# 支付场景参数 (t_pay_scene_param)

## 用途
物理表 `acquireii.t_pay_scene_param`,主键 `global_id, pkey`。支付场景参数。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 通用指令id |
| `pkey` | varchar(200) | 键 |
| `value` | varchar(255) | 值 · 可空 |

## 主键 / 索引
- 主键:`global_id, pkey`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
