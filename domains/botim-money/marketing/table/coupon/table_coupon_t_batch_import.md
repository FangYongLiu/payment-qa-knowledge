---
id: tbl_coupon_t_batch_import
object_type: Table
name: 批量导入表 (t_batch_import)
aliases: [t_batch_import, coupon.t_batch_import]
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

# 批量导入表 (t_batch_import)

## 用途
物理表 `coupon.t_batch_import`,主键 `id`。批量导入表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `batch_no` | varchar(32) | 批次号 |
| `file_name` | varchar(256) | 上传文件名 |
| `file_tag` | varchar(256) | ufs地址 |
| `applier` | varchar(32) | 提交人 |
| `status` | varchar(16) | 状态 CW待校验，CF校验失败，CS校验成功，EW待执行，EP执行中，S成功，F失败 |
| `memo` | varchar(256) | 备注 · 可空 |
| `extension` | varchar(256) | 扩展字段 · 可空 |
| `error_code` | varchar(32) | 错误code · 可空 |
| `error_msg` | text | 错误描述 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
