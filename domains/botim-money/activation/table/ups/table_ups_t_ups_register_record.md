---
id: tbl_ups_t_ups_register_record
object_type: Table
name: 会员注册记录 (t_ups_register_record)
aliases: [t_ups_register_record, ups.t_ups_register_record]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ups schema DDL
tags: [activation, ups]
sensitivity: normal
related_services: []
---

# 会员注册记录 (t_ups_register_record)

## 用途
物理表 `ups.t_ups_register_record`,主键 `id`。会员注册记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `guid` | varchar(32) | 全局标识 |
| `uid` | varchar(64) | 用户唯一标识 |
| `register_mark` | varchar(32) | 手机号.例:+86-13427091218 |
| `partner_id` | varchar(32) | 导入平台id。比如totok的partnerId |
| `owner_id` | varchar(32) | 会员所有者。目前为topay的商户id |
| `mark_type` | varchar(32) | 标识类型，分手机号，邮箱。决定了register_mark的值 |
| `mid` | varchar(32) | 会员号 |
| `has_password` | varchar(2) | 已设置密码为Y.未设置为N |
| `passport` | varchar(32) | 护照号码 |
| `id_number` | varchar(32) | 身份证号 |
| `id_name` | varchar(32) | 身份证姓名 |
| `first_login` | varchar(2) | 是第一次登录为Y · 可空 |
| `user_init` | varchar(2) | 用户自己初始化设置了为Y · 可空 |
| `create_time` | bigint | 创建时间 |
| `update_time` | bigint | 更新时间 |
| `enable_flag` | varchar(2) | 记录是否有效(未作废),Y有效，N为已作废 |

## 主键 / 索引
- 主键:`id`
- `idx_turc_mid`:mid
- `idx_turc_registermark`:register_mark
- `idx_turc_uid`:uid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
