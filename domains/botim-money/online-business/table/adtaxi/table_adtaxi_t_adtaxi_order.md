---
id: tbl_adtaxi_t_adtaxi_order
object_type: Table
name: 出租车订单表 (t_adtaxi_order)
aliases: [t_adtaxi_order, adtaxi.t_adtaxi_order]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: adtaxi schema DDL
tags: [online-business, 出租车支付, adtaxi]
sensitivity: normal
related_services: [svc_adtaxi]
---

# 出租车订单表 (t_adtaxi_order)

## 用途
物理表 `adtaxi.t_adtaxi_order`,主键 `id`。出租车订单。属出租车支付服务 [[svc_adtaxi]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_adtaxi]](= `related_services`)。
- **谁读写它**:出租车支付链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 全局号 |
| `qr_id` | varchar(50) | qrid,仅id |
| `qr_code` | varchar(128) | qrcode完整 · 可空 |
| `currency_code` | varchar(32) | 收单币种 |
| `amount` | decimal(19,4) | 收单金额 |
| `payee_mid` | varchar(32) | 收款人mid |
| `payer_mid` | varchar(32) | 付款人mid · 可空 |
| `acquire_order_id` | bigint | 收单订单号 · 可空 |
| `status` | varchar(16) | 状态 |
| `fail_code` | varchar(32) | 错误码 · 可空 |
| `fail_message` | varchar(128) | 错误描述 · 可空 |
| `paid_time` | timestamp(3) | 支付成功时间 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `unity_result_code` | varchar(64) | 统一结果码 · 可空 |
| `voucher_no` | varchar(32) | 原始凭证 · 可空 |
| `scanner_mid` | varchar(32) | 扫码MID · 可空 |
| `payee_mcc` | varchar(64) | payeeMcc · 可空 |
| `scanner_platform` | varchar(32) | scannerPlatform · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_at_qi`:qr_id (UNIQUE)
- `i_at_ct`:created_time
- `i_at_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发场景校验版本递增。
- **金额精度**:decimal 金额比较用容差(< 0.01);amount 与 currency 需一致。
- **关联收单**:`acquire_order_id` 关联 acquireii 收单订单(跨库,出租车支付走收单)。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
