---
id: tbl_ecollect_t_cart_item
object_type: Table
name: Shopping cart items (per user x shop) (t_cart_item)
aliases: [t_cart_item, ecollect.t_cart_item]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ecollect schema DDL
tags: [wallet, ecollect]
sensitivity: normal
related_services: []
---

# Shopping cart items (per user x shop) (t_cart_item)

## 用途
物理表 `ecollect.t_cart_item`,主键 `id`。Shopping cart items (per user x shop)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | PK |
| `user_id` | varchar(8) | Buyer Botim UID |
| `shop_id` | bigint(21) | Shop ID |
| `product_id` | bigint(21) | Product ID |
| `quantity` | int(8) | Quantity (>0) |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_user_shop`:user_id, shop_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
