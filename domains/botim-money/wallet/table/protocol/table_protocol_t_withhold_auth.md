---
id: tbl_protocol_t_withhold_auth
object_type: Table
name: 协议支付授权表 (t_withhold_auth)
aliases: [t_withhold_auth, protocol.t_withhold_auth]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: protocol schema DDL
tags: [wallet, protocol]
sensitivity: normal
related_services: []
---

# 协议支付授权表 (t_withhold_auth)

## 用途
物理表 `protocol.t_withhold_auth`,主键 `id`。协议支付授权表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `sign_info_id` | bigint(25) | 协议ID |
| `auth_type` | varchar(35) | 授权类型 如：卡，账户，全部；空默认全部 · 可空 |
| `auth_sub_type` | varchar(25) | 授权子类型  如：全卡，单卡，全账户，单账户；空默认全部 · 可空 |
| `authed_user` | varchar(25) | 授权用户 |
| `merchant_id` | varchar(0) | 商户ID |
| `day_quota` | int | 日限额 · 可空 |
| `single_quota` | int | 单笔限额 · 可空 |
| `effective_time` | timestamp | 生效日期 · 可空 |
| `expire_time` | timestamp | 失效日期 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `memo` | varchar(255) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
