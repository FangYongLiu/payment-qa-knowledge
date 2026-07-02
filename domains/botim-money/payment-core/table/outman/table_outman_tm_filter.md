---
id: tbl_outman_tm_filter
object_type: Table
name: filter表 (tm_filter)
aliases: [tm_filter, outman.tm_filter]
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

# filter表 (tm_filter)

## 用途
物理表 `outman.tm_filter`,主键 `FILTER_ID`。filter表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `FILTER_ID` | bigint(32) | 过滤编号 |
| `FILTER_NAME` | varchar(64) | 过滤器名称 |
| `TYPE` | varchar(64) | 类型 |
| `TAG` | varchar(256) | 标签 · 可空 |
| `EXPRESSION` | varchar(1024) | 表达式 · 可空 |
| `TEMPLATE_ID` | decimal(11) | 模版id · 可空 |
| `FILTER_LEVEL` | decimal(5) | 过滤器级别 |
| `IS_SHORT_CIRCUIT` | char | 是否短路 · 可空 |
| `MEMO` | varchar(256) | memo · 可空 |
| `VALID` | char | valid |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 更新时间 · 可空 |
| `OPERATOR` | varchar(32) | 创建人 · 可空 |
| `CONFIRM_OPERATOR` | varchar(32) | 审核人 · 可空 |
| `UPDATE_OPERATROR` | varchar(32) | 修改人 · 可空 |
| `CHANNEL_CODE` | varchar(32) | 渠道编号 |

## 主键 / 索引
- 主键:`FILTER_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
