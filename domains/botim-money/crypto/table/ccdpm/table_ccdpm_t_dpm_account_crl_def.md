---
id: tbl_ccdpm_t_dpm_account_crl_def
object_type: Table
name: 外部账户定义 (t_dpm_account_crl_def)
aliases: [t_dpm_account_crl_def, ccdpm.t_dpm_account_crl_def]
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

# 外部账户定义 (t_dpm_account_crl_def)

## 用途
物理表 `ccdpm.t_dpm_account_crl_def`,主键 `account_type_id`。外部账户定义。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_type_id` | bigint | 账户类型ID · 可空 |
| `account_title_id` | varchar(32) | 账户科目ID · 可空 |
| `account_attribute` | decimal(1) | 账户属性：1:对私,2:对公            9:内部 · 可空 |
| `fund_attribute` | decimal(1) | 资金属性：1:借记,2:贷记/混合 · 可空 |
| `account_type` | decimal(4) | 账户类型：1:基本户,2:一般户,3:专用户,4:临时户,5:保证金户 · 可空 |
| `currency_code` | varchar(10) | 币种 · 可空 |
| `bal_direction` | decimal(1) | 余额方向：1:借,2:贷,0:双向 · 可空 |
| `status` | decimal(1) | 状态：0:有效,1:无效 · 可空 |
| `remark` | varchar(200) | 备注 · 可空 |
| `input_uid` | varchar(32) | 录入人 · 可空 |
| `input_time` | timestamp | 录入时间 · 可空 |
| `check_uid` | varchar(32) | 检查人 · 可空 |
| `check_time` | timestamp | 检查时间 · 可空 |

## 主键 / 索引
- 主键:`account_type_id`
- `idx_account_attribute_type`:account_attribute, account_type

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
