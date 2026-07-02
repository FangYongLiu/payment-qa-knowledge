---
id: tbl_scoupon_t_writeoff_record
object_type: Table
name: 优惠券使用记录表 (t_writeoff_record)
aliases: [t_writeoff_record, scoupon.t_writeoff_record]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: scoupon schema DDL
tags: [marketing, scoupon]
sensitivity: normal
related_services: []
---

# 优惠券使用记录表 (t_writeoff_record)

## 用途
物理表 `scoupon.t_writeoff_record`,主键 `id`。优惠券使用记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键id |
| `member_id` | varchar(32) | 用户id |
| `merchant_id` | bigint | 优惠券虚拟商户id · 可空 |
| `supplier_id` | bigint | 供应商id |
| `store_id` | bigint | 店铺id · 可空 |
| `pin_code` | varchar(32) | 商户pin码 · 可空 |
| `coupon_code` | varchar(32) | 券码 · 可空 |
| `coupon_id` | bigint | 券id · 可空 |
| `coupon_type` | varchar(12) | 券类型，兑换券-GIFT，代金券-CASH，满减券-CUT，折扣券-DISCOUNT · 可空 |
| `coupon_source` | varchar(32) | 券来源：外部商户券（商住自主生成券号）OMC，合作商户券（PAYBY生成券号）-PMC · 可空 |
| `discount_amount` | decimal(19, 4) | 优惠金额 |
| `currency` | char(3) | 币种 |
| `status` | varchar(32) | 状态 |
| `sub_status` | varchar(12) | 子状态 · 可空 |
| `partner_id` | varchar(32) | 核销来源 · 可空 |
| `writeoff_mcht_mid` | varchar(32) | 核销商户id · 可空 |
| `writeoff_mcht_name` | varchar(255) | 核销商户名称 · 可空 |
| `writeoff_store_name` | varchar(255) | 核销店铺名称 · 可空 |
| `writeoff_store_id` | varchar(32) | 核销店铺id · 可空 |
| `settle_amount` | decimal(19, 4) | 结算金额 · 可空 |
| `face_value` | decimal(19, 4) | 面额 |
| `device_id` | varchar(32) | 核销设备id · 可空 |
| `operator` | varchar(32) | 核销操作人 · 可空 |
| `relation_id` | varchar(32) | 关联id · 可空 |
| `relation_type` | varchar(12) | 关联类型 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |
| `finish_time` | timestamp | 订单完成时间 · 可空 |
| `unity_result_code` | varchar(60) | 统一错误码 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
