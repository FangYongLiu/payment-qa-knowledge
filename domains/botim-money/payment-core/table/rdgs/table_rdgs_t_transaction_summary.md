---
id: tbl_rdgs_t_transaction_summary
object_type: Table
name: 交易Summary (t_transaction_summary)
aliases: [t_transaction_summary, rdgs.t_transaction_summary]
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

# 交易Summary (t_transaction_summary)

## 用途
物理表 `rdgs.t_transaction_summary`,主键 `id`。交易Summary。业务语义细节**待补**(表结构来自 DDL)。

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
| `transaction_type` | varchar(6) | 交易类型;refund,trade · 可空 |
| `channel_code` | varchar(12) | 渠道CODE |
| `channel_name` | varchar(100) | 渠道名 |
| `country_code` | char(2) | 渠道所属的国家CODE |
| `country_name` | varchar(100) | 国家名称 |
| `from_amount` | decimal(15, 4) | 总汇款金额 |
| `from_currency` | char(3) | 汇款币种 |
| `order_amount` | decimal(15, 4) | 付款总金额 |
| `refund_amount` | decimal(15, 4) | 退款总金额 |
| `outer_total_amount` | decimal(15, 4) | 外部总额(含费) |
| `corridor_fee` | decimal(15, 4) | 外部渠道总费用 |
| `corridor_currency` | char(3) | 外部渠道总费用币种 · 可空 |
| `exchange_rate` | decimal(15, 8) | 退款或付款平均汇率 |
| `to_amount` | decimal(15, 4) | 总目标金额 |
| `to_currency` | char(3) | 目标币种 |
| `service_charge` | decimal(15, 4) | 内部总费用 · 可空 |
| `vat` | decimal(15, 4) | 税 |
| `revaluation_rate` | decimal(15, 8) | 估计汇率 · 可空 |
| `total_service_charge` | decimal(15, 4) | 总费用含税 · 可空 |
| `to_country_code` | char(2) | 目标汇款国家 |
| `rate_income` | decimal(15, 4) | 汇率加点总收益 · 可空 |
| `receivable_fee` | decimal(15, 4) | 应收总费用 · 可空 |
| `fx_margin_revenue` | decimal(15, 4) | 总汇差收益 · 可空 |
| `gross_revenue` | decimal(15, 4) | 总通道收益 · 可空 |
| `total_profit` | decimal(15, 4) | 损益总收益 · 可空 |
| `transaction_cnt` | int | 交易笔数 |
| `summary_date` | datetime | 交易汇总日期 |
| `start_time` | timestamp | 开始时间 |
| `end_time` | timestamp | 结束时间 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
