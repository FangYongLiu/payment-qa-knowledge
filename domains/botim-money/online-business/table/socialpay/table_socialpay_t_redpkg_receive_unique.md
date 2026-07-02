---
id: tbl_socialpay_t_redpkg_receive_unique
object_type: Table
name: t_redpkg_receive_unique (t_redpkg_receive_unique)
aliases: [t_redpkg_receive_unique, socialpay.t_redpkg_receive_unique]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: socialpay schema DDL
tags: [online-business, socialpay]
sensitivity: normal
related_services: []
---

# t_redpkg_receive_unique (t_redpkg_receive_unique)

## 用途
物理表 `socialpay.t_redpkg_receive_unique`,主键 `ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint | 主键 · 可空 |
| `REDPKG_VOUCHER_NO` | varchar(32) | 红包凭证 |
| `PAYEE_MEMBER_ID` | varchar(32) | 领取人会员ID |

## 主键 / 索引
- 主键:`ID`
- `t_redpkg_receive_unique_vno_mid`:REDPKG_VOUCHER_NO, PAYEE_MEMBER_ID (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
