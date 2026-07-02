---
id: tbl_bill_t_data_sync_progress
object_type: Table
name: 同步进度表 (t_data_sync_progress)
aliases: [t_data_sync_progress, bill.t_data_sync_progress]
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

# 同步进度表 (t_data_sync_progress)

## 用途
物理表 `bill.t_data_sync_progress`,主键 `id`。同步进度表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 进度ID ID · 可空 |
| `status` | varchar(32) | 状态 stop为停止，normal正常 |
| `data_type` | varchar(32) | 数据类型 · 可空 |
| `sync_source` | varchar(100) | 同步自定义参数 · 可空 |
| `app_code` | varchar(32) | 应用code · 可空 |
| `biz_product_code` | varchar(256) | 业务产品码 · 可空 |
| `gmt_sync_begin` | timestamp | 上次成功时间 |
| `gmt_sync_end` | timestamp | 下个截止时间 · 可空 |
| `interval_time` | int | 间隔时间 时间间隔，秒为单位 |
| `delay` | int | 延迟 · 可空 |
| `data_index` | int | 查询到第几条 · 可空 |
| `page_size` | int | 页面最大条数 |
| `error_msg` | varchar(1024) | 错误信息 · 可空 |
| `revison` | bigint | 乐观锁 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
