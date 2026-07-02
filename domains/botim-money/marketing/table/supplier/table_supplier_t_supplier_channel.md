---
id: tbl_supplier_t_supplier_channel
object_type: Table
name: 供应商渠道 (t_supplier_channel)
aliases: [t_supplier_channel, supplier.t_supplier_channel]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: supplier schema DDL
tags: [marketing, supplier]
sensitivity: normal
related_services: []
---

# 供应商渠道 (t_supplier_channel)

## 用途
物理表 `supplier.t_supplier_channel`,主键 `id`。供应商渠道。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(32) | 待补 · 可空 |
| `SUPPLIER_CHANNEL_CODE` | varchar(32) | 渠道编号 |
| `supplier_channel_name` | varchar(64) | 渠道名称 |
| `PROVIDER_CODE` | varchar(32) | 供应商编号 |
| `PRODUCT_CODE` | varchar(32) | 产品编号 |
| `PRODUCT_NAME` | varchar(32) | 产品名称 |
| `STATUS` | varchar(16) | 是否可用：VALID（可用），INVALID（不可用） |
| `min_amount` | decimal(15, 4) | channel最小金额(结算货币单位:AED) |
| `max_amount` | decimal(15, 4) | channel最大金额(结算货币单位:AED) · 可空 |
| `CURRENCY` | varchar(3) | 币种 |
| `Processing_Mode` | varchar(32) | 处理方式(Instance立即处理/Batch稍后处理) |
| `Redemption_Mechanism` | varchar(32) | 话费兑换机制(Immediate立即收到,ReadReceipt用户根据ReceiptText操作，ReadAdditionalInformation 是根据AdditionalInformation操作) |
| `Redemption_Mechanism_text` | varchar(255) | 话费兑换机制第二第三种的操作提示文本 |
| `EXPECT_ARRIVE_TIME` | varchar(16) | 预期到账时间，T+15M表示15分钟到帐，T+1D表示一天到帐，H小时 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 · 可空 |
| `memo` | varchar(1024) | 备注 · 可空 |
| `SUPPLIER_NO` | varchar(32) | 供应商编号 |
| `SUPPLIER_TYPE` | varchar(16) | 供应商类型，Mobile_top_up：手机充值供应商 |
| `Commission_TYPE` | varchar(1) | 佣金类型：G（groovy），R（rate比率）,E(each每笔) · 可空 |
| `Commission_CONTENT` | varchar(2048) | 佣金计算表达式 · 可空 |
| `service_provider` | varchar(32) | 服务提供商 · 可空 |
| `package_type` | varchar(16) | 套餐类型 · 可空 |
| `display_text` | varchar(256) | 渠道展示文案 · 可空 |
| `description_markdown` | varchar(1024) | 渠道产品详细信息 · 可空 |
| `FACE_VALUE` | decimal(15, 4) | 面值 · 可空 |
| `inquiry_available` | varchar(4) | SKU标识 · 可空 |
| `catalog_version` | varchar(16) | catalog版本号 · 可空 |
| `tax_rate` | decimal(15, 4) | 费率 |
| `min_receive_amount` | decimal(15, 4) | channel最小金额(国际单位) |
| `max_receive_amount` | decimal(15, 4) | channel最大金额(国际单位) · 可空 |
| `uat_number` | varchar(64) | 渠道测试账号 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_channelCode_supplierNo`:SUPPLIER_CHANNEL_CODE, SUPPLIER_NO (UNIQUE)
- `idx_providerCode`:PROVIDER_CODE

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
