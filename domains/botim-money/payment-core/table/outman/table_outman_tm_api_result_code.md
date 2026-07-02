---
id: tbl_outman_tm_api_result_code
object_type: Table
name: API结果编码 (tm_api_result_code)
aliases: [tm_api_result_code, outman.tm_api_result_code]
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

# API结果编码 (tm_api_result_code)

## 用途
物理表 `outman.tm_api_result_code`,主键 `API_RESULT_CODE_ID`。API结果编码。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `API_RESULT_CODE_ID` | bigint(32) | 编码ID，SEQ_API_RESULT_CODE |
| `FUND_CHANNEL_CODE` | varchar(32) | 资金源编码 |
| `API_TYPE` | varchar(32) | 接口类型 · 可空 |
| `RESULT_CODE` | varchar(32) | 结果编码 |
| `RESULT_SUB_CODE` | varchar(32) | 结果子编码 · 可空 |
| `EXPRESSION` | varchar(128) | 判断表达式，作为编码映射的一个补充 · 可空 |
| `DESCRIPTION_TEMPLATE` | varchar(256) | 描述模板，如不为空则优先使用 · 可空 |
| `UNITY_RESULT_CODE` | varchar(32) | 统一结果编码 · 可空 |
| `ORDER_STATUS` | char | 订单状态。S（成功），F（失败），P（处理中），W（未知） · 可空 |
| `USE_MAPPING` | char | 是否启用映射。Y（启用），N（不启用） · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `EXTENSION` | varchar(256) | 扩展参数 · 可空 |
| `SYSTEM_CODE` | varchar(32) | 系统编码 · 可空 |

## 主键 / 索引
- 主键:`API_RESULT_CODE_ID`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
