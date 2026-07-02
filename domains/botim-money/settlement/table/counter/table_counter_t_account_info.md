---
id: tbl_counter_t_account_info
object_type: Table
name: 渠道账户维护,用于手续费、增值税结转 (t_account_info)
aliases: [t_account_info, counter.t_account_info]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 渠道账户维护,用于手续费、增值税结转 (t_account_info)

## 用途
物理表 `counter.t_account_info`,主键 `id`。渠道账户维护,用于手续费、增值税结转。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 主键 |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(4) | 业务类型 · 可空 |
| `account_type` | varchar(4) | 账户类型，增值税、手续费 · 可空 |
| `cr_account_no` | varchar(64) | cr账户号 · 可空 |
| `dr_account_no` | varchar(64) | dr账户号 · 可空 |
| `status` | varchar(4) | 启用 停用 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `operator` | varchar(64) | 操作人 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_channel_biz_account`:fund_channel_code, biz_type, account_type (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
