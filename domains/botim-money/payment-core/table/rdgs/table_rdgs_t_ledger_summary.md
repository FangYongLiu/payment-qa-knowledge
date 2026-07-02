---
id: tbl_rdgs_t_ledger_summary
object_type: Table
name: 直连渠道汇款估值汇总 (t_ledger_summary)
aliases: [t_ledger_summary, rdgs.t_ledger_summary]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rdgs schema DDL
tags: [payment-core, rdgs]
sensitivity: normal
related_services: []
---

# 直连渠道汇款估值汇总 (t_ledger_summary)

## 用途
物理表 `rdgs.t_ledger_summary`,主键 `id`。直连渠道汇款估值汇总。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `task_id` | bigint | 报表任务ID |
| `file_tag` | varchar(64) | ufs文件tag · 可空 |
| `channel_code` | varchar(12) | 渠道CODE |
| `channel_name` | varchar(100) | 渠道名 |
| `country_code` | char(2) | 国家CODE |
| `country_name` | varchar(100) | 国家名称 |
| `currency` | char(3) | 本币币种 |
| `foreign_amount` | decimal(15, 4) | 外币总金额 |
| `foreign_currency` | char(3) | 外币币种 |
| `local_amount` | decimal(15, 4) | 本币总金额 |
| `pre_revaluation` | decimal(15, 4) | 预估前余额 |
| `post_revaluation` | decimal(15, 4) | 预估后金额 |
| `revaluation_profit` | decimal(15, 4) | 预估收益 |
| `revaluation_rate` | decimal(15, 8) | 估计汇率 |
| `fcy_opening_balance` | decimal(15, 4) | fcy opening balance · 可空 |
| `fcy_closing_balance` | decimal(15, 4) | fcy closing balance · 可空 |
| `summary_date` | datetime | 汇总日期 |
| `start_time` | timestamp | 开始时间 |
| `end_time` | timestamp | 结束时间 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time
- `idx_summary_date`:summary_date

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
