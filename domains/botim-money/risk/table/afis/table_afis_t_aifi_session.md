---
id: tbl_afis_t_aifi_session
object_type: Table
name: configuration items in database (t_aifi_session)
aliases: [t_aifi_session, afis.t_aifi_session]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: afis schema DDL
tags: [risk, afis]
sensitivity: normal
related_services: []
---

# configuration items in database (t_aifi_session)

## 用途
物理表 `afis.t_aifi_session`,主键 `id`。configuration items in database。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `af_sid` | varchar(50) | the unique ID sent to AiFi system to identify one session group |
| `af_resp` | char(10) | AiFi Oasis API response result: Success|Failure|Unknown |
| `user_type` | char(10) | user type: CardUser|PayByMID |
| `user_account` | varchar(60) | user unique account |
| `device_id` | varchar(60) | device id, POS/Facepay Device |
| `store_id` | int | AiFi Store ID, started at 1 |
| `pre_payment_token` | varchar(100) | pre-auth token or facepay payment token |
| `payment_status` | char(10) | payment status: ToPay|FullPaid|PartialPaid|Failed |
| `payment_memo` | varchar(50) | memo for this session · 可空 |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
