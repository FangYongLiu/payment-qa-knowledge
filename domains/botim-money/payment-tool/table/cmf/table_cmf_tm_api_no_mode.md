---
id: tbl_cmf_tm_api_no_mode
object_type: Table
name: 资金源接口订单号模式 (tm_api_no_mode)
aliases: [tm_api_no_mode, cmf.tm_api_no_mode]
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

# 资金源接口订单号模式 (tm_api_no_mode)

## 用途
物理表 `cmf.tm_api_no_mode`,主键 `API_NO_MODE_ID`。资金源接口订单号模式。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `API_NO_MODE_ID` | decimal(11) | 模式ID |
| `GEN_PATTERN` | varchar(64) | 生成模式 |
| `SEQ_NAME` | varchar(32) | 流水号名称 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`API_NO_MODE_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
