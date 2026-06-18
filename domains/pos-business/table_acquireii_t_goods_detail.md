---
id: tbl_acquireii_t_goods_detail
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_goods_detail.md
tags:
- 商品
- 电商
- 明细表
subdomain: null
module: null
sensitivity: normal
name: 商品明细表
aliases:
- t_goods_detail
- acquireii.t_goods_detail
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

记录订单中的**商品信息**，常见于电商、收银台、ToB 收单场景。

**典型场景**：
- 电商订单包含的商品
- 收银台展示的商品列表
- 风控判断（看商品类目）

表名 `acquireii.t_goods_detail`，字符集 utf8mb4（支持 emoji），重要程度 ⭐⭐⭐。

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `global_id` | bigint | ✅ | 主键，对应订单 global_id |
| `goods_id` | varchar(200) |  | 商品 ID |
| `goods_name` | varchar(200) |  | 商品名 |
| `price` | decimal(19,4) |  | 单价 |
| `price_currency_code` | varchar(50) |  | 单价币种 |
| `quantity` | decimal(19,4) |  | 数量 |
| `goods_category` | varchar(200) |  | 商品类目 |
| `categories_tree` | varchar(200) |  | 类目树（层级路径，用 `/` 分隔，如 `Electronics/Phones/Smartphones`） |
| `body` | varchar(500) |  | 商品描述 |
| `show_url` | varchar(500) |  | 展示 URL（图片或详情页） |

## 主键/索引

- 主键：`PRIMARY (global_id)`
- 关联：与 `t_acquire_order` 1:1，关联字段 `global_id`

## 校验点(QA 关注)

1. **utf8mb4 字符集**：`goods_name` 等字段需支持 emoji 或多语言，验证写入与展示。
2. **1:1 关系**：`global_id` 是主键，一笔订单仅一条记录，不是多行明细——注意与多商品场景的设计差异。
3. **show_url 失效**：商品下架后 URL 可能失效，展示侧需容错。
4. **categories_tree 格式**：层级路径用 `/` 分隔，统计/风控解析时按此约定。
5. **币种一致性**：`price_currency_code` 与订单币种是否一致需校验。
6. **金额精度**：`price`、`quantity` 均为 decimal(19,4)，计算总金额 `price * quantity` 注意精度。
