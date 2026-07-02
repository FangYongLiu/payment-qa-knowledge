---
id: tbl_mchtsettle_t_clearing_fileline_fail
object_type: Table
name: 清算文件行失败表 (t_clearing_fileline_fail)
aliases: [t_clearing_fileline_fail, mchtsettle.t_clearing_fileline_fail]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mchtsettle schema DDL
tags: [online-business, 商户结算, mchtsettle]
sensitivity: normal
related_services: [svc_merchant_settlement]
---

# 清算文件行失败表 (t_clearing_fileline_fail)

## 用途
物理表 `mchtsettle.t_clearing_fileline_fail`,主键 `id`。(DDL 未提供表注释)。属商户结算服务 [[svc_merchant_settlement]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_merchant_settlement]](= `related_services`)。
- **谁读写它**:结算链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | fileLineId |
| `batch_id` | bigint | batchId |
| `status` | varchar(16) | status |
| `merchant_name` | varchar(100) | merchantName · 可空 |
| `mid` | varchar(20) | mid · 可空 |
| `reason` | varchar(255) | reason |
| `sale_amount` | decimal(19,4) | saleAmount |
| `currency` | char(3) | currency |
| `transaction_type` | varchar(32) | transaction_type |
| `fail_type` | varchar(64) | Fail type |
| `created_time` | timestamp(3) | created time |
| `last_updated_time` | timestamp(3) | last update time |
| `data_version` | bigint | bigint |
| `reference_no` | varchar(20) | reference_no · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_batch_id_status`:batch_id, status
- `i_ci_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发场景校验版本递增。
- **金额精度**:decimal 金额比较用容差(< 0.01);amount 与对应 currency 成对、需一致。
- **批次维度**:`batch_id` 关联清算批次 t_clearing_batch。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
