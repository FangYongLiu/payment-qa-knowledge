---
id: tbl_rdgs_t_dealing_summary
object_type: Table
name: 直连渠道换汇汇总 (t_dealing_summary)
aliases: [t_dealing_summary, rdgs.t_dealing_summary]
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

# 直连渠道换汇汇总 (t_dealing_summary)

## 用途
物理表 `rdgs.t_dealing_summary`,主键 `id`。直连渠道换汇汇总。业务语义细节**待补**(表结构来自 DDL)。

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
| `dealing_date` | datetime | 换汇日期;换汇日期YYYYMMDD |
| `from_amount` | decimal(15, 4) | 换汇原金额;换汇时的原金额 |
| `from_currency` | char(3) | 换汇币种;换汇时的币种如USD |
| `to_amount` | decimal(15, 4) | 目标金额;目标金额 |
| `to_currency` | char(3) | 目标币种;目标币种如PKR |
| `local_amount` | decimal(15, 4) | 本币金额;AED金额 |
| `local_currency` | char(3) | 本币种;AED |
| `avg_rate` | decimal(15, 8) | 平均汇率;前一日dealing记录的平均汇率 |
| `dealing_cnt` | int | 换汇笔数 |
| `status` | char | 状态;I:无效,V:有效 |
| `summary_date` | datetime | 汇总日期 |
| `start_time` | timestamp | 开始时间 |
| `end_time` | timestamp | 结束时间 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time
- `idx_dealing_date`:dealing_date

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
