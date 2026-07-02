---
id: tbl_onboarding_t_item_result_param_history
object_type: Table
name: t_item_result_param_history (t_item_result_param_history)
aliases: [t_item_result_param_history, onboarding.t_item_result_param_history]
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

# t_item_result_param_history (t_item_result_param_history)

## 用途
物理表 `onboarding.t_item_result_param_history`,主键 `id`。t_item_result_param_history。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `origin_id` | bigint | t_item_result_param id · 可空 |
| `pkey` | varchar(50) | pkey |
| `value` | varchar(200) | value |
| `data_version` | bigint | data_version · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_origin_id_version`:origin_id, data_version

## 校验点(QA 关注)
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
