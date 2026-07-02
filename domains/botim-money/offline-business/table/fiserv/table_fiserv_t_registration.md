---
id: tbl_fiserv_t_registration
object_type: Table
name: 注册表 (t_registration)
aliases: [t_registration, fiserv.t_registration]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: fiserv schema DDL
tags: [offline-business, fiserv]
sensitivity: normal
related_services: []
---

# 注册表 (t_registration)

## 用途
物理表 `fiserv.t_registration`,主键 `id`。注册表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 自增ID · 可空 |
| `tid` | varchar(32) | Terminal ID |
| `did` | varchar(32) | Datawire · 可空 |
| `STORE_ID` | varchar(32) | STORE ID · 可空 |
| `deviceid` | varchar(32) | Device ID · 可空 |
| `sn` | varchar(32) | Serial Number · 可空 |
| `status` | varchar(32) | SUCCESS 注册成功, RETRY:需要重试 FAIL:失败,需要人工介入 注销(LOGOUT)状态 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_reg_tid_mid`:tid, STORE_ID (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
