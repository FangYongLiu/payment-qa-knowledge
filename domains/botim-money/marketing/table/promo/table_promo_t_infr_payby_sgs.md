---
id: tbl_promo_t_infr_payby_sgs
object_type: Table
name: t_infr_payby_sgs (t_infr_payby_sgs)
aliases: [t_infr_payby_sgs, promo.t_infr_payby_sgs]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: promo schema DDL
tags: [marketing, promo]
sensitivity: normal
related_services: []
---

# t_infr_payby_sgs (t_infr_payby_sgs)

## 用途
物理表 `promo.t_infr_payby_sgs`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `source_id` | char(32) | source id |
| `url` | varchar(100) | url |
| `req_body` | varchar(1024) | request body of rewarding use payby sgs |
| `req_sign` | varchar(512) | request sign of rewarding use payby sgs |
| `req_time` | bigint | request time of rewarding use payby sgs |
| `resp_body` | varchar(1024) | response body of rewarding use payby sgs · 可空 |
| `resp_sign` | varchar(512) | response sign of rewarding use payby sgs · 可空 |
| `resp_time` | bigint | response time of rewarding use payby sgs · 可空 |
| `resp_status` | varchar(30) | response status of rewarding use payby sgs · 可空 |
| `status` | varchar(20) | status of rewarding use payby sgs |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
