---
id: tbl_rdgs_t_revaluation_summary
object_type: Table
name: 直连渠道汇款估值汇总 (t_revaluation_summary)
aliases: [t_revaluation_summary, rdgs.t_revaluation_summary]
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

# 直连渠道汇款估值汇总 (t_revaluation_summary)

## 用途
物理表 `rdgs.t_revaluation_summary`,主键 `id`。直连渠道汇款估值汇总。业务语义细节**待补**(表结构来自 DDL)。

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
| `local_currency` | char(3) | 本币币种 |
| `after_local_amount` | decimal(15, 4) | 总本币余额 |
| `revaluation_amount` | decimal(15, 4) | 估值金额 |
| `margin_amount` | decimal(15, 4) | 汇差收益 |
| `cumulative_margin` | decimal(15, 4) | 月累计利润 |
| `summary_date` | datetime | 汇总日期 |
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
