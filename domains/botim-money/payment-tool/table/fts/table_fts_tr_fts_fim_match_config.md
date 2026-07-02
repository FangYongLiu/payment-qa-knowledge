---
id: tbl_fts_tr_fts_fim_match_config
object_type: Table
name: tr_fts_fim_match_config (tr_fts_fim_match_config)
aliases: [tr_fts_fim_match_config, fts.tr_fts_fim_match_config]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: fts schema DDL
tags: [payment-tool, fts]
sensitivity: normal
related_services: []
---

# tr_fts_fim_match_config (tr_fts_fim_match_config)

## 用途
物理表 `fts.tr_fts_fim_match_config`,主键 `id`。tr_fts_fim_match_config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | unique ID · 可空 |
| `match_type` | varchar(20) | CA/IBAN/PREPAID/OTHER |
| `match_pattern` | varchar(30) | CA: /AE514130001000361101001 payee account,IBAN PATTERN: AEd2 413d 16 payee account, |
| `destination` | varchar(64) | LOCAL/APPLICATION_NAME,query where belong to, regular is a dubbo version |
| `notify_group` | varchar(64) | APPLICATION_NAME, where recharge, regular is a dubbo version |
| `priority` | int(3) | 1-CA,2-IBAN,3-PREPAID CARD,999-OTHER |
| `status` | char | Y,N |
| `gmt_create` | timestamp | create time |
| `gmt_update` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_tffmc_gct`:gmt_create

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
