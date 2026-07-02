---
id: tbl_reconciliation_t_clear_file_flow
object_type: Table
name: 清算文件流水 (t_clear_file_flow)
aliases: [t_clear_file_flow, reconciliation.t_clear_file_flow]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 清算文件流水 (t_clear_file_flow)

## 用途
物理表 `reconciliation.t_clear_file_flow`,主键 `id`。清算文件流水。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `parse_batch_no` | varchar(32) | 清算文件解析批次编号 · 可空 |
| `file_seq_no` | varchar(32) | 文件序号 · 可空 |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `bill_date` | varchar(8) | 对账日期 · 可空 |
| `biz_type` | varchar(16) | 业务类型 I:充值 O:提现 B:退款 · 可空 |
| `file_name` | varchar(256) | 文件名称 · 可空 |
| `file_path` | varchar(512) | 文件路径 包含目录名和文件名 · 可空 |
| `total_record` | int | 总笔数 · 可空 |
| `total_amount` | decimal(15, 2) | 总金额 · 可空 |
| `currency` | varchar(3) | 币种 货币 · 可空 |
| `status` | varchar(4) | 文件解析状态 I:上传完成待解析 S:解析成功  F:解析失败允许再次上传 C:取消(该清算文件对应清算流水已删除) · 可空 |
| `operator` | varchar(32) | 操作员 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 |
| `file_tag` | varchar(64) | ufs文件标志 · 可空 |
| `memo` | varchar(255) | 备注信息 · 可空 |
| `file_type` | varchar(4) | 文件所属类型资金清算文件、手续费交易明细 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
