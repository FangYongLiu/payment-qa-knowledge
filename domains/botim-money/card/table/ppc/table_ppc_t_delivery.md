---
id: tbl_ppc_t_delivery
object_type: Table
name: Delivery (t_delivery)
aliases: [t_delivery, ppc.t_delivery]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Delivery (t_delivery)

## 用途
物理表 `ppc.t_delivery`,主键 `delivery_id`。Delivery。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `delivery_id` | bigint | ID |
| `member_id` | varchar(20) | Member ID |
| `delivery_detail` | varchar(32) | Delivery Detail: JSON Object, Ues encrypt, Include fields: phoneNo, fullName, city, street, address, flatNo |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`delivery_id`
- `idx_member_id`:member_id
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
