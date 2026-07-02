---
id: tbl_gptrade_t_cancel_order
object_type: Table
name: 撤销订单 (t_cancel_order)
aliases: [t_cancel_order, gptrade.t_cancel_order]
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

# 撤销订单 (t_cancel_order)

## 用途
物理表 `gptrade.t_cancel_order`,主键 `cancel_voucher_no`。撤销订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `cancel_voucher_no` | bigint | 撤销凭证号：18位，固定14+10位时间戳+4位序列+2位随机 |
| `cancel_request_no` | bigint | 撤销请求号 |
| `client_id` | varchar(32) | 客户端id |
| `trade_voucher_no` | bigint | 交易凭证号 |
| `cancel_amount` | decimal(19, 4) | 撤销金额 |
| `cancel_status` | varchar(10) | 撤销状态：P=处理中，S=成功，F=失败 |
| `transaction_id` | bigint | 记账事务号 · 可空 |
| `unity_result_code` | varchar(50) | 统一返回码 · 可空 |
| `finish_time` | timestamp | 结束时间 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`cancel_voucher_no`
- `idx_cancel_request_no`:cancel_request_no
- `idx_trade_voucher_no`:trade_voucher_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
