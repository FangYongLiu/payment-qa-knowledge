---
id: tbl_outman_tb_channel_stat
object_type: Table
name: 调用统计表 (tb_channel_stat)
aliases: [tb_channel_stat, outman.tb_channel_stat]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: outman schema DDL
tags: [payment-core, outman]
sensitivity: normal
related_services: []
---

# 调用统计表 (tb_channel_stat)

## 用途
物理表 `outman.tb_channel_stat`,主键 `CHANNEL_STAT_ID`。调用统计表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CHANNEL_STAT_ID` | bigint(32) | 渠道统计编号 |
| `CHANNEL_ID` | bigint(32) | 渠道ID |
| `APP_ID` | varchar(32) | app_id · 可空 |
| `BIZ_PRODUCT_CODE` | varchar(32) | 业务产品码 · 可空 |
| `CNT_TYPE` | varchar(32) | 统计类型(Sys,IDCert) |
| `STAT_CIRCLE` | varchar(32) | 统计周期:YEAR,MONTH,WEEK,DAY,HOUR,10MIN |
| `STAT_DATE` | timestamp | 统计日期 |
| `SUCCESS_CNT` | int | 成功笔数 · 可空 |
| `FAIL_CNT` | int | 失败笔数 · 可空 |
| `TOTAL_CNT` | int | 总笔数 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 更新时间 · 可空 |
| `OVERTIME_CNT` | int | 超时笔数 · 可空 |

## 主键 / 索引
- 主键:`CHANNEL_STAT_ID`
- `uk_stat_cols5`:STAT_DATE, CHANNEL_ID, APP_ID, CNT_TYPE, STAT_CIRCLE (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
