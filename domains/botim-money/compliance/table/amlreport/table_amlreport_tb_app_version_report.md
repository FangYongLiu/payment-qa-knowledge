---
id: tbl_amlreport_tb_app_version_report
object_type: Table
name: app历史 (tb_app_version_report)
aliases: [tb_app_version_report, amlreport.tb_app_version_report]
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

# app历史 (tb_app_version_report)

## 用途
物理表 `amlreport.tb_app_version_report`,主键 `id`。app历史。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `member_id` | varchar(32) | 会员ID · 可空 |
| `device_id` | varchar(128) | 设备ID · 可空 |
| `app_platform` | varchar(50) | 所属平台 payby/botim/totok · 可空 |
| `sdk_version` | varchar(20) | sdk版本 · 可空 |
| `app_version` | varchar(20) | app版本 · 可空 |
| `use_count` | decimal | 使用次数 · 可空 |
| `first_use_time` | timestamp | 第一次使用时间 · 可空 |
| `last_use_time` | timestamp | 最后一次使用时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_app_version_member_id`:member_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
