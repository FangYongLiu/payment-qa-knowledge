---
id: tbl_acquireii_t_goods_detail
object_type: Table
domain: device-pos
status: archived
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
- tbl_acquireii_t_amount_detail
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_promotion_info
- tbl_acquireii_t_sharing_info
related_scenarios:
- scn_acquire_product_apply
- scn_merchant_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_goods_detail`（商品明细表）记录订单中的**商品信息**，常见于电商、收银台、ToB 收单场景。字符集 `utf8mb4`（支持 emoji / 多语言）。重要程度 ⭐⭐⭐。

**典型场景**：
- 电商订单包含的商品
- 收银台展示的商品列表
- 风控判断（看商品类目）

## 在交易链路中的位置

商品明细是收单订单的**业务附属信息**，不参与资金清结算计算，但承载订单的语义（卖什么、多少钱、什么类目）。

```
t_acquire_order (订单主表, global_id)
   ├── t_goods_detail        ← 本表：商品语义信息 (1:1)
   ├── t_amount_detail       ← 金额明细
   ├── t_payment_info        ← 支付信息
   ├── t_promotion_info      ← 优惠券信息
   └── t_sharing_info        ← 分账信息
```

下单时与主单一同写入；风控、对账、客诉、报表等环节按 `global_id` 反查商品语义。

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `global_id` | bigint | ✅ | 主键，对应订单 `t_acquire_order.global_id` |
| `goods_id` | varchar(200) |  | 商品 ID |
| `goods_name` | varchar(200) |  | 商品名 |
| `price` | decimal(19,4) |  | 单价 |
| `price_currency_code` | varchar(50) |  | 单价币种 |
| `quantity` | decimal(19,4) |  | 数量 |
| `goods_category` | varchar(200) |  | 商品类目 |
| `categories_tree` | varchar(200) |  | 类目树（层级路径，用 `/` 分隔，如 `Electronics/Phones/Smartphones`） |
| `body` | varchar(500) |  | 商品描述 |
| `show_url` | varchar(500) |  | 展示 URL（图片或详情页） |

## 主键 / 索引 / 关联

- 主键：`PRIMARY (global_id)`
- 与 `t_acquire_order` **1:1**，关联字段 `global_id`
- 一个订单仅一条记录，不是多商品多行明细结构（如需多商品需另行设计或在 `body` 内聚合）

## QA 落库检查要点

1. **是否落库**：含商品信息的下单请求（电商/收银台），订单成功后 `t_goods_detail` 应有一条记录，`global_id` 与 `t_acquire_order.global_id` 一致。
2. **utf8mb4 字符集**：`goods_name`、`body` 含 emoji 或多语言（中文、阿拉伯文、日文等）时需正确写入与展示，不能乱码或截断。
3. **1:1 关系校验**：同一 `global_id` 不会出现多行；与多商品场景的设计差异在用例评审时需明确（避免误以为是明细行表）。
4. **categories_tree 格式**：层级路径用 `/` 分隔，统计/风控按此约定解析，写入时不应出现非法分隔符。
5. **币种一致性**：`price_currency_code` 应与 `t_acquire_order` / `t_amount_detail` 的订单币种一致，跨币种需关注 DCC 场景。
6. **金额精度**：`price`、`quantity` 均为 `decimal(19,4)`；计算总金额 `price * quantity` 时注意精度，不应与 `t_amount_detail` 的订单金额产生不可解释偏差。
7. **show_url 容错**：商品下架后 URL 可能失效，展示侧需容错；落库本身不应因 URL 校验失败被阻断。
8. **可空字段**：除 `global_id` 外其他字段均可空，渠道未透传时落 NULL 可接受，不应写入空串导致下游解析异常。
9. **关联完整性**：通过 `global_id` 反查 `t_acquire_order` 应能命中，无孤儿记录。