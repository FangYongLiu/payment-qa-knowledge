---
id: tbl_cashdesk_tm_pay_channel_info
object_type: Table
name: 支付渠道定义表 (tm_pay_channel_info)
aliases: [tm_pay_channel_info, cashdesk.tm_pay_channel_info]
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

# 支付渠道定义表 (tm_pay_channel_info)

## 用途
物理表 `cashdesk.tm_pay_channel_info`,主键 `PAY_CHANNEL_CODE`。支付渠道定义表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PAY_CHANNEL_CODE` | varchar(16) | 支付渠道代码,手动配置 |
| `PAY_CHANNEL_NAME` | varchar(32) | 支付渠道名称 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`PAY_CHANNEL_CODE`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
