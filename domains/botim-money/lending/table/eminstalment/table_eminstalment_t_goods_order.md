---
id: tbl_eminstalment_t_goods_order
object_type: Table
name: 商品订单表 (t_goods_order)
aliases: [t_goods_order, eminstalment.t_goods_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: eminstalment schema DDL
tags: [lending, eminstalment]
sensitivity: normal
related_services: []
---

# 商品订单表 (t_goods_order)

## 用途
物理表 `eminstalment.t_goods_order`,主键 `id`。商品订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Id · 可空 |
| `order_no` | varchar(64) | 订单号 |
| `user_id` | varchar(20) | 用户id |
| `platform_user_id` | varchar(50) | 电商平台的用户id |
| `store_order_no` | int | 电商平台的订单号 |
| `amount` | decimal(15, 2) | 电商订单的金额（从content解析得来） |
| `currency` | char(3) | 电商订单的价格的计量货币（从content解析得来） · 可空 |
| `instalment_product_id` | int | 用户在电商下单时选择的分期产品id，对应t_product表的id · 可空 |
| `apply_expire_time` | bigint | 申请过期时间 · 可空 |
| `content` | varchar(4096) | 电商传递过来的订单详情（原请求参数） |
| `md5_content` | varchar(32) | 电商传递过来的订单详情（原请求参数）md5的加密值，用于电商订单滤重 |
| `status` | smallint(4) | 待补 |
| `downpayment_expire_time` | bigint | 首付过期时间 · 可空 |
| `memo` | varchar(255) | 记录订单取消的原因 · 可空 |
| `create_time` | timestamp | 插入时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_mc`:md5_content (UNIQUE)
- `uk_ono`:order_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
