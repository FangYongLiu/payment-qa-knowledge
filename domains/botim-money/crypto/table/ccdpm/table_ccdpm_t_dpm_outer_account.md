---
id: tbl_ccdpm_t_dpm_outer_account
object_type: Table
name: 外部账户 (t_dpm_outer_account)
aliases: [t_dpm_outer_account, ccdpm.t_dpm_outer_account]
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

# 外部账户 (t_dpm_outer_account)

## 用途
物理表 `ccdpm.t_dpm_outer_account`,主键 `account_no`。外部账户。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_no` | varchar(32) | 账户号 |
| `account_title_no` | varchar(32) | 科目号 · 可空 |
| `account_name` | varchar(64) | 账户名称 · 可空 |
| `open_date` | timestamp | 开户日期 · 可空 |
| `member_id` | varchar(15) | 会员号 · 可空 |
| `status_map` | varchar(6) | 账户状态：第一位:激活状态0:未激活1:已激活, 第二位:锁定状态0:未锁定1:已锁定, 第三位:冻结状态0:未冻结1:借方冻结2:贷方冻结3:双向冻结, 第四位:销户状态0:未销户1:已销户2:已结转长期不动户 · 可空 |
| `account_attribute` | decimal(1) | 账户属性：1:对私,2:对公 · 可空 |
| `account_type` | decimal(4) | 账户类型：1:基本户,2:一般户,3:专用户,4:临时户,5:保证金户 · 可空 |
| `curr_bal_direction` | decimal(1) | 当前余额方向：1:借,2:贷 · 可空 |
| `bal_direction` | decimal(1) | 账户余额方向：1:借,2:贷,0:双向 · 可空 |
| `currency_code` | varchar(10) | 货币类型 · 可空 |
| `accounting_version` | bigint | 记账版本 |
| `last_update_time` | timestamp | 更新时间 · 可空 |
| `request_no` | varchar(32) | 开外部户请求号：不可为空 需唯一 |

## 主键 / 索引
- 主键:`account_no`
- `uk_request_no`:request_no (UNIQUE)
- `idx_member_id`:member_id
- `idx_open_date`:open_date

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
