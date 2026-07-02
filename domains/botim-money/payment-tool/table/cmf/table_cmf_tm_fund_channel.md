---
id: tbl_cmf_tm_fund_channel
object_type: Table
name: 资金渠道 (tm_fund_channel)
aliases: [tm_fund_channel, cmf.tm_fund_channel]
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

# 资金渠道 (tm_fund_channel)

## 用途
物理表 `cmf.tm_fund_channel`,主键 `FUND_CHANNEL_CODE`。资金渠道。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `FUND_CHANNEL_CODE` | varchar(32) | 编码 |
| `NAME` | varchar(64) | 名称 |
| `DESCRIPTION` | varchar(256) | 描述 · 可空 |
| `INST_CODE` | varchar(16) | 机构代码 |
| `BIZ_TYPE` | char | 业务类型：I（入款），O（出款） |
| `PAY_MODE` | varchar(16) | 支付方式，如：网银，卡通，线下，手机充值卡，手机话费，微汇卡，积分。。。 |
| `SIGNED_CROP` | char | 签约公司：Y（益充），S（微汇） |
| `STATUS` | varchar(16) | 是否可用：VALID（可用），INVALID（不可用） |
| `VALID_FROM` | timestamp | 有效开始时间 |
| `VALID_TO` | timestamp | 有效截止时间 |
| `MAX_AMOUNT` | decimal(15, 2) | 最大金额 |
| `MIN_AMOUNT` | decimal(15, 2) | 最小金额 |
| `EXPECT_ARRIVE_TIME` | varchar(16) | T+15M表示15分钟到帐，T+1D表示一天到帐，H小时 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `CHANNEL_MODE` | varchar(16) | 渠道模式 · 可空 |
| `PRIORITY` | decimal(2) | 此优先级在过滤，优选之后使用 · 可空 |

## 主键 / 索引
- 主键:`FUND_CHANNEL_CODE`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
