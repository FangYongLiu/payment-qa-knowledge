---
id: tbl_amlreport_tb_ip_report
object_type: Table
name: 用户IP交易统计 (tb_ip_report)
aliases: [tb_ip_report, amlreport.tb_ip_report]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: amlreport schema DDL
tags: [compliance, amlreport]
sensitivity: normal
related_services: []
---

# 用户IP交易统计 (tb_ip_report)

## 用途
物理表 `amlreport.tb_ip_report`,主键 `id`。用户IP交易统计。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `member_id` | varchar(32) | 会员ID · 可空 |
| `ip` | varchar(64) | IP地址 · 可空 |
| `use_count` | decimal | 使用次数 · 可空 |
| `first_use_time` | timestamp | 第一次使用时间 · 可空 |
| `last_use_time` | timestamp | 最后一次使用时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `member_id`:member_id, ip (UNIQUE)
- `idx_ip_report_ip`:ip

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
