---
id: tbl_payment_tb_session_template
object_type: Table
name: 场次模板 (tb_session_template)
aliases: [tb_session_template, payment.tb_session_template]
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

# 场次模板 (tb_session_template)

## 用途
物理表 `payment.tb_session_template`,主键 `SESSION_TEMPLATE_ID`。场次模板。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `SESSION_TEMPLATE_ID` | decimal(11) | 场次模板ID |
| `TEMPLATE_NAME` | varchar(64) | 模板名称 |
| `SESSION_ID_EXPRESSION` | varchar(128) | 场次ID表达式 · 可空 |
| `SESSION_DEFINE` | varchar(64) | 场次定义，触发器表达式 |
| `DELAY_MINUTE` | decimal | 延时时间，单位分钟 |
| `GATHER_TYPE` | char | 汇总类型：N-不汇总；G-汇总；O-轧差；B-批量 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`SESSION_TEMPLATE_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
