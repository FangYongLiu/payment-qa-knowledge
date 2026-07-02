---
id: tbl_pfs_tb_card_bin_0815
object_type: Table
name: 稳定，100000行 (tb_card_bin_0815)
aliases: [tb_card_bin_0815, pfs.tb_card_bin_0815]
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

# 稳定，100000行 (tb_card_bin_0815)

## 用途
物理表 `pfs.tb_card_bin_0815`,主键 `BIN_ID`。稳定，100000行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `BIN_ID` | decimal(15) | BIN系统Id |
| `BANK_CODE` | varchar(32) | 银行编码，如ABC |
| `CARD_TYPE` | varchar(4) | 卡类型：CC=贷记卡，DC=借记卡，SCC=准贷记卡，PC=预付卡 |
| `CARD_NAME` | varchar(256) | 卡种名称 |
| `BIN_NO` | varchar(32) | BIN号 |
| `CARD_LENGTH` | decimal(2) | 卡号长度 |
| `BANK_NO` | varchar(32) | 发卡行代码 · 可空 |
| `EXTENSIONS` | varchar(512) | 扩展信息 · 可空 |
| `ENABLE_FLAG` | char | 启用标识：Y启用，N停用 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `VERSION` | decimal(15) | 版本 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`BIN_ID`
- `UK_CARDBIN_TYPE_BIN_CARDLEN`:BIN_NO, CARD_TYPE, CARD_LENGTH (UNIQUE)
- `I_CARDBIN_BANKCODE`:BANK_CODE

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
