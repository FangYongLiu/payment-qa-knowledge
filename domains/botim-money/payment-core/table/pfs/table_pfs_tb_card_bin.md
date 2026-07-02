---
id: tbl_pfs_tb_card_bin
object_type: Table
name: tb_card_bin (tb_card_bin)
aliases: [tb_card_bin, pfs.tb_card_bin]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pfs schema DDL
tags: [payment-core, pfs]
sensitivity: normal
related_services: []
---

# tb_card_bin (tb_card_bin)

## 用途
物理表 `pfs.tb_card_bin`,主键 `bin_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `bin_id` | int(15) | 卡bin主键 · 可空 |
| `BANK_CODE` | varchar(32) | 待补 |
| `CARD_TYPE` | varchar(4) | 待补 |
| `CARD_NAME` | varchar(256) | 待补 |
| `BIN_NO` | varchar(32) | 待补 |
| `CARD_LENGTH` | decimal(2) | 待补 |
| `BANK_NO` | varchar(32) | 待补 · 可空 |
| `EXTENSIONS` | varchar(512) | 待补 · 可空 |
| `ENABLE_FLAG` | char | 待补 |
| `MEMO` | varchar(256) | 待补 · 可空 |
| `VERSION` | decimal(15) | 待补 |
| `GMT_CREATE` | timestamp | 待补 |
| `GMT_MODIFY` | timestamp | 待补 |

## 主键 / 索引
- 主键:`bin_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
