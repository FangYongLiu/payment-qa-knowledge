---
id: tbl_acquireii_t_pay_scene_param
object_type: Table
name: 支付场景参数表 (t_pay_scene_param)
aliases: [t_pay_scene_param, acquireii.t_pay_scene_param]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquireii schema DDL
tags: [online-business, 收单, acquireii]
sensitivity: normal
related_services: [svc_acquireii]
---

# 支付场景参数表 (t_pay_scene_param)

## 用途
物理表 `acquireii.t_pay_scene_param`,主键 `global_id, pkey`。支付场景参数。属收单服务 [[svc_acquireii]]。业务语义细节**待补**(表结构来自 DDL,用途需结合代码/文档补充)。

## 关联关系
- **所属服务**:[[svc_acquireii]](= `related_services`)。
- **谁读写它**:收单链路的服务 / 接口(由对方文档的 `related_tables` 声明,本表侧不重复)。
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
- **KV 结构**:本表为键值参数表(主键含 `pkey`),具体键集合随业务扩展、**待补**;不要假设固定列。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
