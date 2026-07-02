---
id: tbl_coupon_t_coupon_goods
object_type: Table
name: 优惠券 (t_coupon_goods)
aliases: [t_coupon_goods, coupon.t_coupon_goods]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: coupon schema DDL
tags: [marketing, coupon]
sensitivity: normal
related_services: []
---

# 优惠券 (t_coupon_goods)

## 用途
物理表 `coupon.t_coupon_goods`,主键 `coupon_id`。优惠券。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `coupon_id` | bigint | 主键 |
| `sku_code` | varchar(32) | skuCode · 可空 |
| `coupon_name` | varchar(128) | 区域 |
| `biz_name` | varchar(64) | 内部展示优惠券名字 · 可空 |
| `coupon_tag` | varchar(64) | 优惠券标签 · 可空 |
| `batch_no` | varchar(32) | 批次号 · 可空 |
| `category_id` | varchar(32) | 分类 |
| `value_desc` | varchar(255) | 价值描述 · 可空 |
| `face_value` | decimal(19, 4) | 面额 |
| `original_price` | decimal(19, 4) | 原价 |
| `prevailing_price` | decimal(19, 4) | 现价 |
| `discount_amount` | decimal(19, 4) | 优惠额度 |
| `sales_channel` | varchar(12) | 销售渠道 online/offline |
| `publish_count` | bigint | 发布张数 · 可空 |
| `currency` | char(3) | 币种 |
| `supplier_id` | bigint | 供应商id |
| `merchant_id` | bigint | 商户id · 可空 |
| `coupon_logo` | varchar(255) | 优惠券图标 · 可空 |
| `coupon_img` | varchar(255) | 优惠券图片 · 可空 |
| `status` | varchar(12) | 状态 初始化：INIT；已使用：USED；已锁定：LOCKED |
| `desc` | varchar(1024) | 描述 · 可空 |
| `rules` | text | 规则 · 可空 |
| `tips` | varchar(255) | 使用提示 · 可空 |
| `index` | int | 排序 · 可空 |
| `coupon_type` | varchar(12) | 券类型，兑换券-GIFT，代金券-CASH，满减券-CUT，折扣券-DISCOUNT · 可空 |
| `sku_count` | int(12) | 库存 · 可空 |
| `strategy_type` | varchar(32) | COMMON_CUT：普通满减；LOOP_CUT：累计满减；DISCOUNT：折扣 · 可空 |
| `upper_limit` | decimal(12, 4) | 使用上限 · 可空 |
| `threshold` | decimal(12, 4) | 使用门槛 · 可空 |
| `coupon_source` | varchar(12) | 券来源，外部商户券（商住自主生成券号）OMC，合作商户券（PAYBY生成券号）-PMC，PAYBY券（PAYBY生成券号）-SOC,(自营券) · 可空 |
| `source` | varchar(12) | basis；merchant · 可空 |
| `platform` | varchar(64) | 支持平台;totok-pay,payby,botim-pay · 可空 |
| `expiry_type` | varchar(12) | 计算失效时间类型 DURATION：时长；RANGE：范围 · 可空 |
| `expiry_value` | int(12) | 生效时长（单位：分钟） · 可空 |
| `writeoff_method` | varchar(12) | 券核销方式，直接核销-DW，内部交易结算核销-ISW，商户交易结算核销-MSW · 可空 |
| `payment_acct` | varchar(32) | 出金账户 · 可空 |
| `use_url` | varchar(128) | 使用跳转地址 · 可空 |
| `detail_url` | varchar(64) | 券详情跳转地址 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |
| `effective_time` | timestamp | 生效时间 · 可空 |
| `expired_time` | timestamp | 过期时间 · 可空 |

## 主键 / 索引
- 主键:`coupon_id`
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
