---
id: tbl_cmf_tm_fund_channel_settle
object_type: Table
name: 资金渠道算信息 (tm_fund_channel_settle)
aliases: [tm_fund_channel_settle, cmf.tm_fund_channel_settle]
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

# 资金渠道算信息 (tm_fund_channel_settle)

## 用途
物理表 `cmf.tm_fund_channel_settle`,主键 `SETTLE_ID`。资金渠道算信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `SETTLE_ID` | int unsigned | 结算ID · 可空 |
| `FUND_CHANNEL_CODE` | varchar(32) | 资金源编码 |
| `CONTRACT_NO` | varchar(64) | 合同号 |
| `MERCHANT_NO` | varchar(64) | 商户号 |
| `ACCOUNT_NO` | varchar(64) | 结算账号 · 可空 |
| `ACCOUNT_NAME` | varchar(128) | 结算帐户名称 · 可空 |
| `SETTLE_MODE` | char | 结算方式：S（单笔），B（批量） |
| `SETTLE_CYCLE` | decimal(3) | 结算周期，以天为单位的数字 · 可空 |
| `CLEARING_FILE_MODE` | char | 清算文件获取支持模式：N（不支持），F（FTP），O（线上），U（线下） |
| `ENABLE` | char | 是否可用：Y（可用），N（不可用） |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `EXTENSION` | varchar(256) | 扩展 · 可空 |

## 主键 / 索引
- 主键:`SETTLE_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
