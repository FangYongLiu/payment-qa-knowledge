---
id: tbl_acquire_t_auth_code
object_type: Table
name: 授权代码 (t_auth_code)
aliases: [t_auth_code, acquire.t_auth_code]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquire schema DDL
tags: [offline-business, acquire]
sensitivity: normal
related_services: []
---

# 授权代码 (t_auth_code)

## 用途
物理表 `acquire.t_auth_code`,主键 `global_id`。授权代码。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | varchar(200) | 全局id |
| `auth_code` | varchar(200) | 授权码字符串 |
| `pay_method` | varchar(200) | 选择的支付渠道 · 可空 |
| `risk_level` | varchar(200) | 风险级别 |

## 主键 / 索引
- 主键:`global_id`
- `uk_ac_ac`:auth_code (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
