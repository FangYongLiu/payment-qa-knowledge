---
id: tbl_transfer_t_redpkg_order
object_type: Table
name: 红包订单 (t_redpkg_order)
aliases: [t_redpkg_order, transfer.t_redpkg_order]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: transfer schema DDL
tags: [wallet, transfer]
sensitivity: normal
related_services: []
---

# 红包订单 (t_redpkg_order)

## 用途
物理表 `transfer.t_redpkg_order`,主键 `redpkg_no`。红包订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `redpkg_no` | bigint(18) | 主键 |
| `out_trade_no` | varchar(64) | 商户红包单号 |
| `partner_id` | varchar(32) | 商户ID |
| `payment_no` | bigint(18) | 付款单号 |
| `amount` | decimal(15, 4) | 金额 |
| `currency` | varchar(10) | 币种 |
| `type` | varchar(20) | 红包类型：AVERAGE,LUCKY,PERSONAL |
| `subject` | varchar(100) | 主题 · 可空 |
| `payer_uid` | varchar(32) | 付款人uid |
| `status` | varchar(20) | 红包状态 WAIT_PAY,PAY_SUCCESS,REFUND,COMPLETE |
| `payer_mid` | varchar(32) | 付款人mid |
| `redpkg_count` | int(4) | 红包个数 |
| `lucy_member_id` | varchar(32) | 手气最佳 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `self_receive` | tinyint | 是否可自己领取 |
| `attribute` | varchar(20) | 红包属性 PRIVATE: 私有 PUBLIC: 公开 · 可空 |
| `extension` | varchar(500) | 扩展参数 · 可空 |

## 主键 / 索引
- 主键:`redpkg_no`
- `uk_red_payment_no`:payment_no (UNIQUE)
- `uk_rp_partner_id_out_trade_no`:partner_id, out_trade_no (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
