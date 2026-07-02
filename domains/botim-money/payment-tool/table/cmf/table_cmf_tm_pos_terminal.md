---
id: tbl_cmf_tm_pos_terminal
object_type: Table
name: POS终端信息 (tm_pos_terminal)
aliases: [tm_pos_terminal, cmf.tm_pos_terminal]
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

# POS终端信息 (tm_pos_terminal)

## 用途
物理表 `cmf.tm_pos_terminal`,主键 `TERMINAL_ID`。POS终端信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `TERMINAL_ID` | decimal(6) | 终端ID |
| `POS_CODE` | varchar(16) | 终端代码 |
| `POS_KEY` | varchar(1024) | 终端密钥 · 可空 |
| `FUND_CHANNEL_CODE` | varchar(32) | 资金渠道编码 |
| `STATUS` | char | 状态。I：已签到；B：已关帐；O：空闲/已签退 |
| `ENABLE` | char | 是否可用。Y：是；N：否 |
| `SETTLE_TIME_PATTERN` | varchar(16) | 结算时间表达式，cron表达式 · 可空 |
| `SUBMIT_MAX_NUM` | decimal(5) | 上送最大笔数 · 可空 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `MERCHANT_NO` | varchar(32) | 商品编号 · 可空 |

## 主键 / 索引
- 主键:`TERMINAL_ID`
- `UIDX_PT_PC_FC`:FUND_CHANNEL_CODE, POS_CODE (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
