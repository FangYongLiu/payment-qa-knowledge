---
id: tbl_outman_tm_filter_node
object_type: Table
name: 节点信息表 (tm_filter_node)
aliases: [tm_filter_node, outman.tm_filter_node]
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

# 节点信息表 (tm_filter_node)

## 用途
物理表 `outman.tm_filter_node`,主键 `NODE_ID`。节点信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `NODE_ID` | bigint(32) | 节点编号 |
| `FILTER_ID` | bigint(32) | 过滤编号 |
| `NODE_TYPE` | varchar(16) | 节点类型 |
| `NODE_NAME` | varchar(64) | 节点显示名称 |
| `NODE_VALUE` | varchar(4000) | 节点值,支持多个，之间用","分隔 |
| `NODE_CONDITION` | varchar(32) | 筛选条件,指定是否包含节点值 |
| `MEMO` | varchar(256) | memo · 可空 |
| `GMT_CREATE` | timestamp | gmt_create |
| `GMT_MODIFIED` | timestamp | gmt_modified · 可空 |
| `OPERATOR` | varchar(32) | 创建人 · 可空 |
| `CONFIRM_OPERATOR` | varchar(32) | 审核人 · 可空 |
| `UPDATE_OPERATROR` | varchar(32) | 修改人 · 可空 |

## 主键 / 索引
- 主键:`NODE_ID`
- `INDEX_NODE_ID_UNIT_ID`:NODE_ID, FILTER_ID

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
