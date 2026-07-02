---
id: tbl_pfs_tb_data_check_config
object_type: Table
name: 数据校验配置表 (tb_data_check_config)
aliases: [tb_data_check_config, pfs.tb_data_check_config]
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

# 数据校验配置表 (tb_data_check_config)

## 用途
物理表 `pfs.tb_data_check_config`,主键 `id`。数据校验配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `product_code` | varchar(32) | 支付产品码 · 可空 |
| `refund_flag` | char | 退款标示（N正常交易 R退款交易） · 可空 |
| `amount_expression` | varchar(500) | 校验表达式 · 可空 |
| `status` | char | 状态（N无效 Y有效） · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
