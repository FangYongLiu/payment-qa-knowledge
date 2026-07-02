---
id: tbl_upic_t_trade_relate_order
object_type: Table
name: 交易关联号 (t_trade_relate_order)
aliases: [t_trade_relate_order, upic.t_trade_relate_order]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: upic schema DDL
tags: [card, upic]
sensitivity: normal
related_services: []
---

# 交易关联号 (t_trade_relate_order)

## 用途
物理表 `upic.t_trade_relate_order`,主键 `trade_request_no`。交易关联号。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trade_request_no` | bigint | 交易请求号 |
| `transaction_type` | varchar(10) | 记账类型：DEBIT=借记，CREDIT=贷记，REVERSAL=冲正 |
| `trx_voucher_no` | bigint | 交易业务凭证 |
| `trade_type` | varchar(10) | 交易类型：REFUND=退款，TRANSFER=转账 |
| `trade_order_status` | varchar(10) | 状态：P=处理中，S=成功，F=失败 · 可空 |
| `unity_result_code` | varchar(64) | 统一返回码 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |
| `finish_time` | timestamp | 结束时间 · 可空 |

## 主键 / 索引
- 主键:`trade_request_no`
- `idx_update_time`:update_time
- `idx_voucher_no`:trx_voucher_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
