---
id: tbl_gptrade_t_trade_order_extend
object_type: Table
name: 交易订单扩展 (t_trade_order_extend)
aliases: [t_trade_order_extend, gptrade.t_trade_order_extend]
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

# 交易订单扩展 (t_trade_order_extend)

## 用途
物理表 `gptrade.t_trade_order_extend`,主键 `trade_voucher_no`。交易订单扩展。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trade_voucher_no` | bigint | 交易凭证号：18位，固定14+10位时间戳+4位序列+2位随机 |
| `description` | varchar(255) | 商品描述 |
| `cashier_biz_type` | varchar(32) | 收银台业务类型 · 可空 |
| `cashier_payee` | varchar(20) | 收银台收款方 · 可空 |
| `cashier_return_url` | varchar(255) | 收银台返回地址 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`trade_voucher_no`
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
