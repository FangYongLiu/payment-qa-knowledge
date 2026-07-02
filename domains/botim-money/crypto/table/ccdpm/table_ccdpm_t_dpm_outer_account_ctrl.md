---
id: tbl_ccdpm_t_dpm_outer_account_ctrl
object_type: Table
name: 外部开户约束表 (t_dpm_outer_account_ctrl)
aliases: [t_dpm_outer_account_ctrl, ccdpm.t_dpm_outer_account_ctrl]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccdpm schema DDL
tags: [crypto, ccdpm]
sensitivity: normal
related_services: []
---

# 外部开户约束表 (t_dpm_outer_account_ctrl)

## 用途
物理表 `ccdpm.t_dpm_outer_account_ctrl`,主键 `request_no`。外部开户约束表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `request_no` | varchar(32) | 开外部户请求号：不可为空 需唯一 |
| `member_id` | varchar(32) | 会员ID |
| `currency` | varchar(10) | 币种 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 最后修改时间 |

## 主键 / 索引
- 主键:`request_no`
- `uk_member_id_currency`:member_id, currency (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
