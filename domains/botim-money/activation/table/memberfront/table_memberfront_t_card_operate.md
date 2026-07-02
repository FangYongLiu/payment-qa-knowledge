---
id: tbl_memberfront_t_card_operate
object_type: Table
name: 卡操作表 (t_card_operate)
aliases: [t_card_operate, memberfront.t_card_operate]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: memberfront schema DDL
tags: [activation, memberfront]
sensitivity: normal
related_services: []
---

# 卡操作表 (t_card_operate)

## 用途
物理表 `memberfront.t_card_operate`,主键 `id`。卡操作表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 |
| `operate_type` | char | 操作类型 B:绑卡、U:解绑卡 |
| `member_id` | varchar(32) | 会员ID |
| `partner_id` | varchar(32) | 商户ID |
| `order_no` | bigint | 订单号 · 可空 |
| `card_id` | bigint | 操作的卡ID |
| `card_token` | varchar(64) | 卡Token · 可空 |
| `extension` | varchar(512) | 操作的参数, JSON · 可空 |
| `notify_url` | varchar(255) | 通知地址 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 修改时间 |
| `auth_method` | varchar(16) | 绑卡授权方式 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_gmt_create`:gmt_create
- `uk_order_no`:order_no

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
