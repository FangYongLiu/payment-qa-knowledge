---
id: tbl_cmf_tb_notify_3ds_result
object_type: Table
name: tb_notify_3ds_result (tb_notify_3ds_result)
aliases: [tb_notify_3ds_result, cmf.tb_notify_3ds_result]
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

# tb_notify_3ds_result (tb_notify_3ds_result)

## 用途
物理表 `cmf.tb_notify_3ds_result`,主键 `result_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `result_id` | bigint(32) | 结果id |
| `card_token_id` | bigint(32) | 卡token的id · 可空 |
| `channel_code` | varchar(32) | 渠道编号 |
| `inst_order_no` | varchar(32) | 机构订单号 |
| `trade_order_no` | varchar(32) | 交易订单号 · 可空 |
| `payment_order_no` | varchar(32) | 支付订单号 · 可空 |
| `eci` | char(2) | eci结果 · 可空 |
| `identity_result` | char | 认证结果 · 可空 |
| `identity_result_desc` | varchar(32) | 认证结果描述 · 可空 |
| `extension` | varchar(128) | 扩展参数 · 可空 |
| `gmt_cmf_request` | timestamp | 请求cmf时间 · 可空 |
| `gmt_bank_request` | timestamp | 请求渠道时间 · 可空 |
| `gmt_bank_response` | timestamp | 渠道响应时间 · 可空 |

## 主键 / 索引
- 主键:`result_id`
- `uk_3ds_order_no`:inst_order_no (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
