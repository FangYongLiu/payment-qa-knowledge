---
id: tbl_transfer_t_merchant_transfer_order
object_type: Table
name: Merchant Transfer Order (t_merchant_transfer_order)
aliases: [t_merchant_transfer_order, transfer.t_merchant_transfer_order]
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

# Merchant Transfer Order (t_merchant_transfer_order)

## 用途
物理表 `transfer.t_merchant_transfer_order`,主键 `id`。Merchant Transfer Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID: 前八后九 |
| `trade_request_no` | bigint | Trade Request No |
| `request_order_no` | varchar(64) | Request Order No |
| `merchant_id` | varchar(20) | Merchant ID |
| `receive_id` | varchar(20) | Receive ID |
| `currency` | char(3) | Currency |
| `amount` | decimal(19, 4) | Transfer Amount |
| `status` | char(2) | Status: C=订单创建,W=等待领取,SI=结算中,S=领取成功,RI=撤销中,R=撤销 |
| `expire_time` | timestamp | Expire Time |
| `receive_extend` | varchar(100) | Receiver Extend · 可空 |
| `memo` | varchar(255) | Order Description · 可空 |
| `biz_source` | varchar(30) | Business Source · 可空 |
| `callback_url` | varchar(255) | Callback Url · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`id`
- `uk_trade_request_no`:trade_request_no (UNIQUE)
- `idx_expire_time`:expire_time
- `idx_request_order_no`:request_order_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
