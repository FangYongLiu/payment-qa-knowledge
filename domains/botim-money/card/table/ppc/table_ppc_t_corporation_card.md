---
id: tbl_ppc_t_corporation_card
object_type: Table
name: Corporation Virtual Card (t_corporation_card)
aliases: [t_corporation_card, ppc.t_corporation_card]
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

# Corporation Virtual Card (t_corporation_card)

## 用途
物理表 `ppc.t_corporation_card`,主键 `corporation_id`。Corporation Virtual Card。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `corporation_id` | varchar(50) | Corporation ID |
| `corporation_name` | varchar(50) | Corporation Name |
| `virtual_card_id` | bigint | Corporation Virtual Card ID |
| `proxy_number` | varchar(20) | Proxy Number |
| `merchant_id` | varchar(20) | Merchant ID |
| `charge_code` | varchar(20) | Charge Code · 可空 |
| `delivery_id` | bigint | Delivery ID: Delivery ID · 可空 |
| `status` | varchar(10) | Status: N=Normal, C=Closed |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`corporation_id`
- `uk_virtual_card_id`:virtual_card_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
