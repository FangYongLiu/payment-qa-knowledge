---
id: tbl_vis_t_transaction_extra_data
object_type: Table
name: 交易信息额外数据表 (t_transaction_extra_data)
aliases: [t_transaction_extra_data, vis.t_transaction_extra_data]
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

# 交易信息额外数据表 (t_transaction_extra_data)

## 用途
物理表 `vis.t_transaction_extra_data`,主键 `id`。交易信息额外数据表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键id · 可空 |
| `transaction_id` | bigint(19) | 流水id |
| `type` | char | 类型 |
| `fragment` | int | 分片 |
| `data` | varchar(1024) | 数据内容 |
| `memo` | varchar(255) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_transactionid_type_fragment`:transaction_id, type, fragment (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
