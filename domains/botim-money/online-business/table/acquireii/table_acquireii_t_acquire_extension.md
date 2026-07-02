---
id: tbl_acquireii_t_acquire_extension
object_type: Table
name: t_acquire_extension (t_acquire_extension)
aliases: [t_acquire_extension, acquireii.t_acquire_extension]
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

# t_acquire_extension (t_acquire_extension)

## 用途
物理表 `acquireii.t_acquire_extension`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | global id |
| `extension` | varchar(255) | Extension · 可空 |
| `data_version` | bigint | data version |
| `created_time` | timestamp(3) | create date |
| `last_updated_time` | timestamp(3) | last update date |
| `pay_extension` | varchar(2048) | Payment extension · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
