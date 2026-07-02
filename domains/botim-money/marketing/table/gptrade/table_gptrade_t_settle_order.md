---
id: tbl_gptrade_t_settle_order
object_type: Table
name: 结算订单 (t_settle_order)
aliases: [t_settle_order, gptrade.t_settle_order]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: gptrade schema DDL
tags: [marketing, gptrade]
sensitivity: normal
related_services: []
---

# 结算订单 (t_settle_order)

## 用途
物理表 `gptrade.t_settle_order`,主键 `settle_voucher_no`。结算订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `settle_voucher_no` | bigint | 结算凭证号：18位，固定14+10位时间戳+4位序列+2位随机 |
| `settle_request_no` | bigint | 结算请求号 |
| `client_id` | varchar(32) | 客户端id |
| `trade_voucher_no` | bigint | 交易凭证号 |
| `is_auto_settle` | char | 是否自动结算：Y=是，N=否 |
| `payee_account_identity` | varchar(32) | 收款方账户标志 |
| `payee_account_type` | varchar(10) | 收款方账户类型 |
| `settle_amount` | decimal(19, 4) | 结算金额 |
| `settle_status` | varchar(10) | 结算状态：I=未生效，P=处理中，S=成功，F=失败 |
| `transaction_id` | bigint | 记账事务号 · 可空 |
| `unity_result_code` | varchar(50) | 统一返回码 · 可空 |
| `finish_time` | timestamp | 结束时间 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(64) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`settle_voucher_no`
- `idx_settle_request_no`:settle_request_no
- `idx_trade_voucher_no`:trade_voucher_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
