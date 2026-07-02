---
id: tbl_cmf_tt_inst_batch_order
object_type: Table
name: 机构归档批次表 (tt_inst_batch_order)
aliases: [tt_inst_batch_order, cmf.tt_inst_batch_order]
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

# 机构归档批次表 (tt_inst_batch_order)

## 用途
物理表 `cmf.tt_inst_batch_order`,主键 `ARCHIVE_BATCH_ID`。机构归档批次表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ARCHIVE_BATCH_ID` | decimal(19) | 批次ID |
| `ARCHIVE_TEMPLATE_ID` | decimal(5) | 归档模板ID · 可空 |
| `ARCHIVE_TYPE` | char | 归档类型：F（文件），M（消息） · 可空 |
| `ORDER_TYPE` | char | 订单类型：I（入款），B（退款），O（出款） |
| `FUND_CHANNEL_CODE` | varchar(36) | 资金渠道编码 |
| `FUND_CHANNEL_API` | varchar(48) | 资金渠道API |
| `PAY_MODE` | varchar(16) | 支付方式：网上银行支付、一点充支付、手机充值卡支付、手机话费支付、手机支付、线下支付（网点支付、邮政支付）、微汇卡支付、积分支付、固话支付、宽带支付、银联快捷支付（银行卡无磁有密支付） · 可空 |
| `TOTAL_AMOUNT` | decimal(15, 2) | 总金额 |
| `TOTAL_COUNT` | decimal(15) | 总笔数 |
| `CURRENCY` | char(3) | 币种 |
| `STATUS` | char | 状态：A：待归档,G--已经归档,S--已经提交,R--已经返回,F--提交失败,P--暂停 |
| `IS_LOCKED` | char | 是否已锁定，锁定则不允许重新生成：Y（是），N（否） · 可空 |
| `FILE_PATH` | varchar(128) | 文件路径 · 可空 |
| `OPERATOR` | varchar(32) | 操作员 · 可空 |
| `GMT_ARCHIVE` | timestamp | 归档时间 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `CHECK_FLAG` | char | 复核文件回导审批结果 · 可空 |
| `BATCH_ORDER_NO` | varchar(64) | 订单批次号 · 可空 |
| `QUERY_TIMES` | decimal(3) | 查询次数 · 可空 |
| `GMT_NEXT_RETRY` | timestamp | 下次重试时间 · 可空 |
| `extension` | varchar(1024) | 扩展参数 · 可空 |

## 主键 / 索引
- 主键:`ARCHIVE_BATCH_ID`
- `I_T_IT_BH_ORDER_GMT_ARC`:GMT_ARCHIVE

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
