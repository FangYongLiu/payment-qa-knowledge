---
id: tbl_payment_tb_clearing_session_map
object_type: Table
name: tb_clearing_session_map (tb_clearing_session_map)
aliases: [tb_clearing_session_map, payment.tb_clearing_session_map]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: payment schema DDL
tags: [payment-core, payment]
sensitivity: normal
related_services: []
---

# tb_clearing_session_map (tb_clearing_session_map)

## 用途
物理表 `payment.tb_clearing_session_map`,主键 `CLEARING_SESSION_ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CLEARING_SESSION_ID` | varchar(32) | 场次ID格式:8位日期+15位0+9位序列 |
| `MD5_SESSION_ID` | varchar(32) | md5场次ID |

## 主键 / 索引
- 主键:`CLEARING_SESSION_ID`
- `UK_CLEARING_S_M_MD5`:MD5_SESSION_ID (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
