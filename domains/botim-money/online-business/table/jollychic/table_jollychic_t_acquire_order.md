---
id: tbl_jollychic_t_acquire_order
object_type: Table
name: 收单订单：收单订单 (t_acquire_order)
aliases: [t_acquire_order, jollychic.t_acquire_order]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: jollychic schema DDL
tags: [online-business, jollychic]
sensitivity: normal
related_services: []
---

# 收单订单：收单订单 (t_acquire_order)

## 用途
物理表 `jollychic.t_acquire_order`,主键 `global_id`。收单订单：收单订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | varchar(32) | 全局唯一 |
| `derive_status` | varchar(32) | 获取状态：CREATED,PLACED · 可空 |
| `deliver_status` | varchar(32) | 发货状态 · 可空 |
| `deliver_time` | timestamp | 发货时间 · 可空 |
| `trade_status` | varchar(32) | 交易状态 |
| `product_code` | varchar(32) | 产品码 |
| `pay_method` | varchar(32) | 支付方式 · 可空 |
| `tx_time` | timestamp | 交易完成时间 · 可空 |
| `aquire_amount` | decimal(19, 4) | 收单金额 |
| `acquire_currency` | varchar(32) | 收单币种 |
| `buyer_mid` | varchar(32) | 购买人MID · 可空 |
| `seller_mid` | varchar(32) | 售卖人MID · 可空 |
| `payee_mid` | varchar(32) | 收款人mid |
| `payer_mid` | varchar(32) | 付款人mid · 可空 |
| `expired_time` | timestamp | 超时时间 · 可空 |
| `notify_url` | varchar(200) | 后端回调地址 · 可空 |
| `redirct_url` | varchar(200) | 前端跳转地址 · 可空 |
| `settlement_currency` | varchar(32) | 结算币种：AED，如果空则按照收单币种取值 · 可空 |
| `subject` | varchar(200) | 商品名称 · 可空 |
| `submit_time` | timestamp | 提交时间：格式：2019-09-24T12:46:33.254+0000 |
| `request_identity` | varchar(255) | 请求标识 |
| `ugc_content` | varchar(512) | 用户生成内容 · 可空 |
| `pay_channel` | varchar(255) | 支付渠道：BALANCE 基本户  BANKCARD 银行卡 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
