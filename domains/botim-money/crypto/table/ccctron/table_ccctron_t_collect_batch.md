---
id: tbl_ccctron_t_collect_batch
object_type: Table
name: 归集批次(不分区) (t_collect_batch)
aliases: [t_collect_batch, ccctron.t_collect_batch]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccctron schema DDL
tags: [crypto, ccctron]
sensitivity: normal
related_services: []
---

# 归集批次(不分区) (t_collect_batch)

## 用途
物理表 `ccctron.t_collect_batch`,主键 `id`。归集批次(不分区)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id(yyyyMMdd999999999) |
| `start_time` | timestamp(3) | 开始时间 |
| `end_time` | timestamp(3) | 结束时间 |
| `included_event_count` | int | 事件计数 |
| `fail_collect_address_count` | int | 失败归集地址个数 · 可空 |
| `success_collect_address_count` | int | 成功归集地址个数 · 可空 |
| `total_collect_address_count` | int | 总共归集地址个数 · 可空 |
| `status` | varchar(50) | 订单状态 |
| `fail_code` | varchar(50) | 失败代码 · 可空 |
| `fail_message` | varchar(200) | 失败消息 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `i_cb_et`:end_time
- `i_cb_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
