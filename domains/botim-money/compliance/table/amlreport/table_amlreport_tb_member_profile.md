---
id: tbl_amlreport_tb_member_profile
object_type: Table
name: 会员账号画像结果 (tb_member_profile)
aliases: [tb_member_profile, amlreport.tb_member_profile]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: amlreport schema DDL
tags: [compliance, amlreport]
sensitivity: normal
related_services: []
---

# 会员账号画像结果 (tb_member_profile)

## 用途
物理表 `amlreport.tb_member_profile`,主键 `member_id`。会员账号画像结果。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `member_id` | varchar(20) | 会员id |
| `eid` | varchar(20) | eid · 可空 |
| `mobile` | varchar(20) | 认证手机号 · 可空 |
| `create_time` | timestamp | 会员创建时间 · 可空 |
| `user_level` | varchar(20) | 会员等级 NORMAL/VIP · 可空 |
| `set_password` | char | 是否设置支付密码Y/N · 可空 |
| `pay_card_num` | int | 支付卡数量 · 可空 |
| `last_deposit_time` | timestamp | 最后一次成功充值时间 · 可空 |
| `last_device_id` | varchar(64) | 最后一次登录设备id · 可空 |
| `last_update_time` | timestamp | 最近一次更新时间 · 可空 |

## 主键 / 索引
- 主键:`member_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
