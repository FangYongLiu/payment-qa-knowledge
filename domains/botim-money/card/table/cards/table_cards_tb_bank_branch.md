---
id: tbl_cards_tb_bank_branch
object_type: Table
name: 分支行 (tb_bank_branch)
aliases: [tb_bank_branch, cards.tb_bank_branch]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cards schema DDL
tags: [card, cards]
sensitivity: normal
related_services: []
---

# 分支行 (tb_bank_branch)

## 用途
物理表 `cards.tb_bank_branch`,主键 `BRANCH_ID`。分支行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `BRANCH_ID` | int | 分支行id · 可空 |
| `COUNTRY_CODE` | varchar(2) | 国家编码 |
| `BANK_CODE` | varchar(128) | 银行编码 |
| `CITY` | varchar(32) | 城市 |
| `BRANCH_NAME` | varchar(128) | 分支行 |
| `SWIFT_CODE` | varchar(11) | swift编码 |
| `ENABLE_FLAG` | varchar(1) | 启用状态 Y-启用 N-禁用 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `EXTENSION` | varchar(256) | 扩展参数 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`BRANCH_ID`
- `uk_swift_code`:SWIFT_CODE (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
