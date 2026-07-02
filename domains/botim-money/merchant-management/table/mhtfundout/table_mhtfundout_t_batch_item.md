---
id: tbl_mhtfundout_t_batch_item
object_type: Table
name: 批量条目 (t_batch_item)
aliases: [t_batch_item, mhtfundout.t_batch_item]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mhtfundout schema DDL
tags: [merchant-management, mhtfundout]
sensitivity: normal
related_services: []
---

# 批量条目 (t_batch_item)

## 用途
物理表 `mhtfundout.t_batch_item`,主键 `id`。批量条目。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `type` | varchar(50) | 订单类型 |
| `beneficiary_id` | bigint | 受益人id · 可空 |
| `batch_order_id` | bigint | 批次订单号 |
| `line_no` | bigint | 行号 |
| `single_order_id` | varchar(50) | 单笔订单号 · 可空 |
| `status` | varchar(200) | 状态 |
| `fail_code` | varchar(200) | 错误码 · 可空 |
| `fail_message` | varchar(200) | 错误描述 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `unity_result_code` | varchar(200) | 统一结果码 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_fbi_line`:batch_order_id, line_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
