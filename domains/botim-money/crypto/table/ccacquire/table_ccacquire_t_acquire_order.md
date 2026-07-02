---
id: tbl_ccacquire_t_acquire_order
object_type: Table
name: 收单数据 (t_acquire_order)
aliases: [t_acquire_order, ccacquire.t_acquire_order]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccacquire schema DDL
tags: [crypto, ccacquire]
sensitivity: normal
related_services: []
---

# 收单数据 (t_acquire_order)

## 用途
物理表 `ccacquire.t_acquire_order`,主键 `global_id`。收单数据。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `request_no` | varchar(200) | 等同于requestIdentity.requestNo.查询方便 |
| `voucher_no` | varchar(200) | 凭证号 · 可空 |
| `device_id` | varchar(200) | 发起方设备id · 可空 |
| `partner_id` | varchar(200) | 发起方memberId |
| `product_code` | varchar(200) | 产品码 |
| `ttlamt_currency_code` | varchar(50) | 收单币种 |
| `total_amount` | decimal(23, 8) | 收单金额 |
| `payee_mid` | varchar(200) | 收款人mid |
| `subject` | varchar(200) | 标题 · 可空 |
| `expired_time` | timestamp(3) | 过期时间 |
| `notify_url` | varchar(500) | 商户通知地址 · 可空 |
| `pay_scene_code` | varchar(32) | 支付场景代码 |
| `status` | varchar(200) | 收单状态 |
| `request_time` | timestamp(3) | 商户声明请求时间 |
| `revoked` | varchar(8) | 待补 · 可空 |
| `reserved` | varchar(200) | 待补 · 可空 |
| `fail_code` | varchar(50) | 错误码 · 可空 |
| `fail_message` | varchar(200) | 错误描述 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `unity_result_code` | varchar(200) | 统一结果码 · 可空 |

## 主键 / 索引
- 主键:`global_id`
- `i_ao_ct`:created_time
- `i_ao_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
