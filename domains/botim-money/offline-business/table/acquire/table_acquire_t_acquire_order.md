---
id: tbl_acquire_t_acquire_order
object_type: Table
name: 收单数据 (t_acquire_order)
aliases: [t_acquire_order, acquire.t_acquire_order]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquire schema DDL
tags: [offline-business, acquire]
sensitivity: normal
related_services: []
---

# 收单数据 (t_acquire_order)

## 用途
物理表 `acquire.t_acquire_order`,主键 `global_id`。收单数据。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `partner_id` | varchar(200) | 合作伙伴mid |
| `product_code` | varchar(200) | 产品码 |
| `product_code_alias` | varchar(200) | 产品码别名 |
| `acquire_currency_code` | varchar(50) | 收单币种代码 |
| `acquire_amount` | decimal(19, 4) | 收单金额 |
| `settlement_currency_code` | varchar(50) | 产品码别名 · 可空 |
| `payee_mid` | varchar(200) | 收款人mid |
| `payer_mid` | varchar(200) | 付款人mid · 可空 |
| `buyer_mid` | varchar(200) | 买方mid · 可空 |
| `seller_mid` | varchar(200) | 卖方mid · 可空 |
| `subject` | varchar(200) | 商品名称 · 可空 |
| `expired_time` | timestamp(3) | 过期时间 · 可空 |
| `notify_url` | varchar(500) | 商户通知地址 · 可空 |
| `redirect_url` | varchar(500) | 前端跳转地址 · 可空 |
| `pay_scene_code` | varchar(32) | 支付场景 |
| `derive_status` | varchar(200) | 收单状态 |
| `submitted_time` | timestamp(3) | 提交时间 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `settlement_amount` | decimal(19, 4) | 结算金额 |

## 主键 / 索引
- 主键:`global_id`
- `i_ao_lut`:last_updated_time
- `i_ao_st`:submitted_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
