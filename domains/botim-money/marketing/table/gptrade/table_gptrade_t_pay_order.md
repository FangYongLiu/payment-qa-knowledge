---
id: tbl_gptrade_t_pay_order
object_type: Table
name: 修改时间 (t_pay_order)
aliases: [t_pay_order, gptrade.t_pay_order]
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

# 修改时间 (t_pay_order)

## 用途
物理表 `gptrade.t_pay_order`,主键 `pay_voucher_no`。修改时间。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `pay_voucher_no` | bigint | 付款凭证号：18位，固定14+10位时间戳+4位序列+2位随机 |
| `pay_request_no` | bigint | 付款请求号 |
| `client_id` | varchar(32) | 客户端id |
| `trade_voucher_no` | bigint | 交易凭证号 |
| `pay_entrance` | varchar(32) | 支付入口 |
| `verify_items` | varchar(128) | 验证项 |
| `pay_status` | varchar(10) | 支付状态：P=处理中，S=成功，F=失败，RP=回滚中，RS=回滚成功 |
| `transaction_id` | bigint | 记账事务号 · 可空 |
| `unity_result_code` | varchar(50) | 统一返回码 · 可空 |
| `finish_time` | timestamp | 结束时间 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `create_time` | timestamp(3) | 创建时间 |
| `update_time` | timestamp(3) | 待补 |

## 主键 / 索引
- 主键:`pay_voucher_no`
- `idx_pay_request_no`:pay_request_no
- `idx_trade_voucher_no`:trade_voucher_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
