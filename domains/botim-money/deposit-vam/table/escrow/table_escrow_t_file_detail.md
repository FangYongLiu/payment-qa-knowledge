---
id: tbl_escrow_t_file_detail
object_type: Table
name: 文件解析详情表 (t_file_detail)
aliases: [t_file_detail, escrow.t_file_detail]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 文件解析详情表 (t_file_detail)

## 用途
物理表 `escrow.t_file_detail`,主键 `detail_id`。文件解析详情表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `detail_id` | bigint(19) | 详情ID |
| `member_id` | varchar(32) | 会员编号 |
| `escrow_amount` | decimal(19, 4) | 存管金额 · 可空 |
| `account_amount` | decimal(19, 4) | 账户金额 · 可空 |
| `currency` | varchar(8) | 币种 · 可空 |
| `direction` | varchar(16) | 方向 · 可空 |
| `detail_type` | varchar(16) | 详情类型 · 可空 |
| `detail_date` | date | 对账日期 |
| `status` | varchar(4) | 对账状态,S-对账成功，F-对账失败 · 可空 |
| `file_id` | bigint(19) | 文件ID |
| `memo` | varchar(2048) | memo · 可空 |
| `card_id` | varchar(32) | 卡ID · 可空 |
| `card_no` | varchar(32) | 卡号 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改日期 · 可空 |
| `bank_code` | varchar(8) | 银行编号 |
| `source_info` | varchar(1024) | 源信息 · 可空 |
| `target_info` | varchar(1024) | 目标信息 · 可空 |

## 主键 / 索引
- 主键:`detail_id`
- `idx_file_detail_clearing`:file_id, detail_type

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
