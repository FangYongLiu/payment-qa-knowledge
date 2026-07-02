---
id: tbl_cmf_tm_heart_monitor
object_type: Table
name: tm_heart_monitor (tm_heart_monitor)
aliases: [tm_heart_monitor, cmf.tm_heart_monitor]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cmf schema DDL
tags: [payment-tool, cmf]
sensitivity: normal
related_services: []
---

# tm_heart_monitor (tm_heart_monitor)

## 用途
物理表 `cmf.tm_heart_monitor`,主键 `MONITOR_ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `MONITOR_ID` | decimal(8) | 监控ID |
| `CHANNEL_NAME` | varchar(64) | 渠道名称 |
| `INST_ORDER_ID` | decimal(15) | 机构订单ID · 可空 |
| `ENABLE` | char | 激活 · 可空 |

## 主键 / 索引
- 主键:`MONITOR_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
