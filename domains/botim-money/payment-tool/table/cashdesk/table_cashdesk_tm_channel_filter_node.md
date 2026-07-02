---
id: tbl_cashdesk_tm_channel_filter_node
object_type: Table
name: 渠道过滤节点，同一单元下的不同节点为“与”关系 (tm_channel_filter_node)
aliases: [tm_channel_filter_node, cashdesk.tm_channel_filter_node]
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

# 渠道过滤节点，同一单元下的不同节点为“与”关系 (tm_channel_filter_node)

## 用途
物理表 `cashdesk.tm_channel_filter_node`,主键 `NODE_ID`。渠道过滤节点，同一单元下的不同节点为“与”关系。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `NODE_ID` | decimal | 节点ID,初始信息手动配置 |
| `UNIT_ID` | decimal | 单元ID |
| `NODE_TYPE` | varchar(36) | 节点类型 |
| `NODE_VALUE` | varchar(400) | 节点值,支持多个，之间用","分隔 |
| `CONDITION` | varchar(10) | 筛选条件,指定是否包含节点值. |
| `GMT_CREATE` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`NODE_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
