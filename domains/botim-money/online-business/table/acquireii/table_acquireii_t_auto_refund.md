---
id: tbl_acquireii_t_auto_refund
object_type: Table
name: 自动退款表 (t_auto_refund)
aliases: [t_auto_refund, acquireii.t_auto_refund]
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

# 自动退款表 (t_auto_refund)

## 用途
物理表 `acquireii.t_auto_refund`,主键 `global_id`。（DDL 未提供表注释）。属收单服务 [[svc_acquireii]]。业务语义细节**待补**(表结构来自 DDL,用途需结合代码/文档补充)。

## 关联关系
- **所属服务**:[[svc_acquireii]](= `related_services`)。
- **谁读写它**:收单链路的服务 / 接口(由对方文档的 `related_tables` 声明,本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | acquire global id |
| `trade_routing` | varchar(50) | trade routing · 可空 |
| `status` | varchar(24) | status · 可空 |
| `created_time` | timestamp(3) | created time · 可空 |
| `last_updated_time` | timestamp(3) | last update time · 可空 |
| `data_version` | bigint | data version · 可空 |

## 主键 / 索引
- 主键:`global_id`
- `i_status_created_time`:status, created_time

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引,勿混用。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发场景校验版本递增、防覆盖。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
