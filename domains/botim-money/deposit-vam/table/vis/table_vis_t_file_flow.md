---
id: tbl_vis_t_file_flow
object_type: Table
name: 文件记录表 (t_file_flow)
aliases: [t_file_flow, vis.t_file_flow]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: vis schema DDL
tags: [deposit-vam, vis]
sensitivity: normal
related_services: []
---

# 文件记录表 (t_file_flow)

## 用途
物理表 `vis.t_file_flow`,主键 `file_id`。文件记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `file_id` | bigint(17) | 主键 |
| `file_type` | varchar(8) | 文件类型 · 可空 |
| `file_date` | date | 日期 · 可空 |
| `oss_path` | varchar(128) | ufs文件名称 · 可空 |
| `status` | varchar(8) | 状态 · 可空 |
| `message` | varchar(128) | 消息记录 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `operator` | varchar(64) | 操作者 · 可空 |
| `carry_over_order` | varchar(32) | 结转单号 · 可空 |
| `confirmer` | varchar(64) | 确认者 · 可空 |
| `gmt_complete` | timestamp | 完成时间 · 可空 |
| `carry_over_amount` | decimal(19, 4) | 结转金额 · 可空 |
| `memo` | varchar(128) | memo · 可空 |
| `carry_over_status` | varchar(8) | 结转状态 · 可空 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |

## 主键 / 索引
- 主键:`file_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
