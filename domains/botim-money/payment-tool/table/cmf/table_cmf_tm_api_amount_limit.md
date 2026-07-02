---
id: tbl_cmf_tm_api_amount_limit
object_type: Table
name: 渠道api限额信息 (tm_api_amount_limit)
aliases: [tm_api_amount_limit, cmf.tm_api_amount_limit]
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

# 渠道api限额信息 (tm_api_amount_limit)

## 用途
物理表 `cmf.tm_api_amount_limit`,主键 `LIMIT_ID`。渠道api限额信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `LIMIT_ID` | int(12) | 限制ID · 可空 |
| `API_CODE` | varchar(16) | 接口编码 |
| `DBCR` | varchar(32) | 借贷标识(DC,CC,GC) · 可空 |
| `INST_CODE` | varchar(32) | 目标机构(ICBC,BOC,...)/(移动,联通,电信) · 可空 |
| `MIN_AMOUNT` | decimal(18, 2) | 最小金额 · 可空 |
| `MAX_AMOUNT` | decimal(18, 2) | 最大金额 · 可空 |
| `currency` | char(3) | 币种 |
| `FACE_LIMIT` | varchar(256) | 允许面值(卡面值10,20,50) · 可空 |
| `MATCH_CONDITION` | varchar(1024) | 匹配条件 · 可空 |
| `SHOW_EXPRESSION` | varchar(2048) | 展示表达式,velocity格式,转义后用于前端显示 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 · 可空 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |
| `AMOUNT_LIMIT_TYPE` | char | 金额限制类型：S-单笔 D-日限额 · 可空 |

## 主键 / 索引
- 主键:`LIMIT_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
