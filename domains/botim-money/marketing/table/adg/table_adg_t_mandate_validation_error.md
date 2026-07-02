---
id: tbl_adg_t_mandate_validation_error
object_type: Table
name: Mandate Validation Error Log (t_mandate_validation_error)
aliases: [t_mandate_validation_error, adg.t_mandate_validation_error]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: adg schema DDL
tags: [marketing, adg]
sensitivity: normal
related_services: []
---

# Mandate Validation Error Log (t_mandate_validation_error)

## 用途
物理表 `adg.t_mandate_validation_error`,主键 `id`。Mandate Validation Error Log。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | unique id · 可空 |
| `dds_ref_no` | varchar(127) | mandate id by dds · 可空 |
| `mandate_create_error` | varchar(2000) | a json object where each field describe the list of error as string associated with a input field in the create request · 可空 |
| `mandate_cancel_error` | varchar(2000) | a json object where each field describe the list of error as string associated with a input field in the cancel request · 可空 |
| `create_time` | timestamp | entry create time |
| `update_time` | timestamp | last update time |

## 主键 / 索引
- 主键:`id`
- `uk_dds_ref_no`:dds_ref_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
