---
id: tbl_cashdesk_tr_filter_scene
object_type: Table
name: 策略支付场景关系 (tr_filter_scene)
aliases: [tr_filter_scene, cashdesk.tr_filter_scene]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cashdesk schema DDL
tags: [payment-tool, cashdesk]
sensitivity: normal
related_services: []
---

# 策略支付场景关系 (tr_filter_scene)

## 用途
物理表 `cashdesk.tr_filter_scene`,主键 `ID`。策略支付场景关系。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint(10) | 主键 · 可空 |
| `SCENE_CODE` | varchar(16) | 支付场景 |
| `FILTER_ID` | decimal | 策略id |
| `GMT_CREATE` | timestamp | 创建日期 · 可空 |

## 主键 / 索引
- 主键:`ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
