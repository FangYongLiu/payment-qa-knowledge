---
id: tbl_mhtfundout_t_fundout_batch_summary
object_type: Table
name: t_fundout_batch_summary (t_fundout_batch_summary)
aliases: [t_fundout_batch_summary, mhtfundout.t_fundout_batch_summary]
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

# t_fundout_batch_summary (t_fundout_batch_summary)

## 用途
物理表 `mhtfundout.t_fundout_batch_summary`,主键 `global_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `content_line_count` | int | 文件内容行数 · 可空 |
| `valid_count` | int | 合法条目计数 · 可空 |
| `success_count` | int | 成功条目计数 · 可空 |
| `valid_amount` | decimal(19, 4) | 合法付款金额 · 可空 |
| `valid_currency` | varchar(50) | 合法付款币种 · 可空 |
| `success_amount` | decimal(19, 4) | 成功付款金额 · 可空 |
| `success_currency` | varchar(50) | 成功付款币种 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `fee_amount` | decimal(19, 4) | 手续费 · 可空 |
| `fee_currency` | varchar(50) | 手续费币种 · 可空 |
| `invalid_item_file_id` | varchar(50) | 无效条目文件id · 可空 |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
