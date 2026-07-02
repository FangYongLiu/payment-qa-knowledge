---
id: tbl_vis_t_iban_apply
object_type: Table
name: iban申请记录 (t_iban_apply)
aliases: [t_iban_apply, vis.t_iban_apply]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: vis schema DDL
tags: [deposit-vam, vis]
sensitivity: normal
related_services: []
---

# iban申请记录 (t_iban_apply)

## 用途
物理表 `vis.t_iban_apply`,主键 `apply_id`。iban申请记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `apply_id` | int(16) | 请求id · 可空 |
| `request_batch_no` | varchar(32) | 批次请求号 |
| `bank_code` | varchar(5) | Bank Code · 可空 |
| `apply_num` | smallint(8) | 请求数量 |
| `response_num` | smallint(8) | 响应数量 · 可空 |
| `status` | char | 状态 · 可空 |
| `response_code` | varchar(32) | 响应码 · 可空 |
| `response_msg` | varchar(64) | 响应信息 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `request_type` | char | 请求类型,N:新创建;M:修改 · 可空 |

## 主键 / 索引
- 主键:`apply_id`
- `uk_iban_apply_batch_no`:request_batch_no (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
