---
id: tbl_payment_tb_biz_product_map
object_type: Table
name: 业务产品编码映射配置，稳定，100行 (tb_biz_product_map)
aliases: [tb_biz_product_map, payment.tb_biz_product_map]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: payment schema DDL
tags: [payment-core, payment]
sensitivity: normal
related_services: []
---

# 业务产品编码映射配置，稳定，100行 (tb_biz_product_map)

## 用途
物理表 `payment.tb_biz_product_map`,主键 `id`。业务产品编码映射配置，稳定，100行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `BIZ_PRODUCT_CODE` | varchar(32) | 业务产品编码 |
| `PRODUCT_CODE` | varchar(32) | 产品编码 |
| `PAYER_FEE_STRATEGY` | varchar(10) | 付款方费用策略 · 可空 |
| `CONTROL_PARAM` | varchar(100) | 控制参数，多个用逗号隔开 · 可空 |
| `ENABLE_FLAG` | char | Y=有效，N=无效 |
| `MEMO` | varchar(512) | 备注 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `UK_BIZPC_PFS`:BIZ_PRODUCT_CODE, PAYER_FEE_STRATEGY (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
