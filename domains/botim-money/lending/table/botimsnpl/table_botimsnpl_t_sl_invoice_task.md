---
id: tbl_botimsnpl_t_sl_invoice_task
object_type: Table
name: 创建发票记录表，用于失败补偿 (t_sl_invoice_task)
aliases: [t_sl_invoice_task, botimsnpl.t_sl_invoice_task]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# 创建发票记录表，用于失败补偿 (t_sl_invoice_task)

## 用途
物理表 `botimsnpl.t_sl_invoice_task`,主键 `id`。创建发票记录表，用于失败补偿。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `busi_entity_no` | varchar(255) | 发票关联的业务主体no，这里所说的业务主体是指众多发票都归于**的，如cashnow的借款订单号 |
| `ref_busi_no` | varchar(64) | 与发票对应的业务的唯一标识 |
| `type` | smallint(4) | 待补 |
| `detail` | varchar(1024) | 调用发票接口用到的参数，json格式 · 可空 |
| `status` | smallint(4) | 待补 |
| `invoice_nos` | varchar(64) | 发票号或tcn号,tcn号可能是多个，用英文逗号分隔 · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `ix_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
