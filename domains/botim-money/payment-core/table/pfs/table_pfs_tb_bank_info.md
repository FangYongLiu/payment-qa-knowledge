---
id: tbl_pfs_tb_bank_info
object_type: Table
name: 稳定，100行 (tb_bank_info)
aliases: [tb_bank_info, pfs.tb_bank_info]
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

# 稳定，100行 (tb_bank_info)

## 用途
物理表 `pfs.tb_bank_info`,主键 `BANK_CODE`。稳定，100行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `BANK_CODE` | varchar(32) | 银行编码，如ABC |
| `BANK_SHORTNAME` | varchar(128) | 银行简称 |
| `BANK_ALIASES` | varchar(256) | 银行别名 · 可空 |
| `UNIFIED_BANK_NO` | char(3) | 行别代码 |
| `EXTENSIONS` | varchar(512) | 扩展信息 · 可空 |
| `ENABLE_FLAG` | char | 启用标识 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `VERSION` | decimal(15) | 版本 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`BANK_CODE`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
