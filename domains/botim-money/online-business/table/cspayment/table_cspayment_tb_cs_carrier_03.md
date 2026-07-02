---
id: tbl_cspayment_tb_cs_carrier_03
object_type: Table
name: 清结算载体 (tb_cs_carrier_03)
aliases: [tb_cs_carrier_03, cspayment.tb_cs_carrier_03]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cspayment schema DDL
tags: [online-business, cspayment]
sensitivity: normal
related_services: []
---

# 清结算载体 (tb_cs_carrier_03)

## 用途
物理表 `cspayment.tb_cs_carrier_03`,主键 `PAYMENT_SEQ_NO, PS_ID, CLEARING_CODE, REQUEST_TYPE`。清结算载体。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `REQUEST_NO` | varchar(32) | 请求号 |
| `AGREEMENT_ID` | decimal(11) | 协议ID，主键:SEQ_CLEARING_AGREEMENT |
| `PAYMENT_SEQ_NO` | varchar(32) | 支付流水号 |
| `PS_ID` | decimal(15) | 流程配置ID |
| `PRE_PS_ID` | decimal(15) | 原流程配置ID · 可空 |
| `CLEARING_CODE` | varchar(32) | 清算代码 |
| `REQUEST_TYPE` | varchar(16) | 请求类型 |
| `CLEARING_SESSION_ID` | varchar(32) | 清算场次标识:SEQ_CLEARING_SESSION_ID · 可空 |
| `STATUS` | char | 状态：W-待结算；P-结算中；S-结算成功；F-结算失败； |
| `SUMMARY` | varchar(128) | 摘要 · 可空 |
| `NOTIFY_STATUS` | char | 通知状态 W-待通知；P-通知中；S-成功； · 可空 |
| `result_code` | varchar(50) | 结果代码 · 可空 |
| `RESULT_MESSAGE` | varchar(128) | 结果信息 · 可空 |
| `EXTENSION` | varchar(1000) | 扩展信息 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`PAYMENT_SEQ_NO, PS_ID, CLEARING_CODE, REQUEST_TYPE`
- `UK_CSC_REQUEST_NO_03`:REQUEST_NO (UNIQUE)
- `IDX_CSC_GMT_MODIFIED_03`:GMT_MODIFIED
- `IDX_CSC_SESSION_ID_03`:CLEARING_SESSION_ID

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
