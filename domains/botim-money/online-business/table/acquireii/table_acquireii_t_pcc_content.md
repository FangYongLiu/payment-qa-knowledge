---
id: tbl_acquireii_t_pcc_content
object_type: Table
name: 支付授权凭证表 (t_pcc_content)
aliases: [t_pcc_content, acquireii.t_pcc_content]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquireii schema DDL
tags: [online-business, 收单, acquireii]
sensitivity: normal
related_services: [svc_acquireii]
---

# 支付授权凭证表 (t_pcc_content)

## 用途
物理表 `acquireii.t_pcc_content`,主键 `global_id`。支付授权凭证。属收单服务 [[svc_acquireii]]。业务语义细节**待补**(表结构来自 DDL,用途需结合代码/文档补充)。

## 关联关系
- **所属服务**:[[svc_acquireii]](= `related_services`)。
- **谁读写它**:收单链路的服务 / 接口(由对方文档的 `related_tables` 声明,本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局id |
| `pcc_final` | varchar(200) | 授权码字符串 |
| `pay_method` | varchar(200) | 选择的支付渠道 · 可空 |
| `risk_level` | varchar(200) | 风险级别 · 可空 |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
