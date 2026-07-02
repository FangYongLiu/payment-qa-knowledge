---
id: tbl_bill_t_data_sync_progress_his
object_type: Table
name: 同步进度表历史 (t_data_sync_progress_his)
aliases: [t_data_sync_progress_his, bill.t_data_sync_progress_his]
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

# 同步进度表历史 (t_data_sync_progress_his)

## 用途
物理表 `bill.t_data_sync_progress_his`,主键 `id`。同步进度表历史。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID · 可空 |
| `ref_id` | int | 关联的进度ID |
| `data_type` | varchar(32) | 数据类型 数据接口类型，默认BILL · 可空 |
| `app_code` | varchar(32) | 应用编码 接口路由使用 · 可空 |
| `gmt_sync_begin` | timestamp | 同步开始时间 |
| `gmt_sync_end` | timestamp | 同步结束时间 |
| `intervel_time` | int | 间隔时间 · 可空 |
| `delay` | int | 延迟 · 可空 |
| `data_count` | int | 同步记录数 分页记录数之和 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
