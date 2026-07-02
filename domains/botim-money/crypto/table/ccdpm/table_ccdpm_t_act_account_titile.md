---
id: tbl_ccdpm_t_act_account_titile
object_type: Table
name: 会计科目 (t_act_account_titile)
aliases: [t_act_account_titile, ccdpm.t_act_account_titile]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccdpm schema DDL
tags: [crypto, ccdpm]
sensitivity: normal
related_services: []
---

# 会计科目 (t_act_account_titile)

## 用途
物理表 `ccdpm.t_act_account_titile`,主键 `title_seq_no`。会计科目。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `title_seq_no` | bigint | 科目序号 · 可空 |
| `title_code` | varchar(16) | 科目代码 |
| `title_name` | varchar(128) | 科目名称 |
| `title_level` | decimal(2) | 科目级别 · 可空 |
| `parent_title_code` | varchar(16) | 父科目 · 可空 |
| `currency` | varchar(10) | 币种 · 可空 |
| `is_leaf` | char | 是否叶子节点：Y: 是 N: 否 · 可空 |
| `type` | char | 类型：1:资产类,2:负债类,3:所有者权益,4:共同类,5:损益类 |
| `balance_direction` | decimal(1) | 余额方向：1:借,2:贷,0:双向 |
| `status` | char | 状态：Y（有效）；N（无效） |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 最后修改时间 |
| `memo` | varchar(128) | 备注 · 可空 |
| `title_range` | decimal(1) | 科目范围：1:内部科目,2:外部科目 |

## 主键 / 索引
- 主键:`title_seq_no`
- `uk_title_code`:title_code (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
