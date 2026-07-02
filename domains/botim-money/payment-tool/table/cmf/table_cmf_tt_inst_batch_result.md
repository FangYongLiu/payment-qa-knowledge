---
id: tbl_cmf_tt_inst_batch_result
object_type: Table
name: 机构批次处理结果 (tt_inst_batch_result)
aliases: [tt_inst_batch_result, cmf.tt_inst_batch_result]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cmf schema DDL
tags: [payment-tool, cmf]
sensitivity: normal
related_services: []
---

# 机构批次处理结果 (tt_inst_batch_result)

## 用途
物理表 `cmf.tt_inst_batch_result`,主键 `BATCH_RESULT_ID`。机构批次处理结果。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `BATCH_RESULT_ID` | decimal(19) | 批次结果ID |
| `ARCHIVE_BATCH_ID` | decimal(19) | 归档批次ID |
| `BATCH_TYPE` | char | 批次类型：C（复核批次）；R（结果批次） · 可空 |
| `FUND_CHANNEL_CODE` | varchar(32) | 资金渠道 |
| `TOTAL_COUNT` | decimal | 总笔数 |
| `TOTAL_AMOUNT` | decimal(15, 2) | 总金额 |
| `CURRENCY` | char(3) | 币种 · 可空 |
| `SUCCESS_COUNT` | decimal | 成功笔数 · 可空 |
| `SUCCESS_AMOUNT` | decimal(15, 2) | 成功金额 · 可空 |
| `FAILED_COUNT` | decimal | 失败笔数 · 可空 |
| `FAILED_AMOUNT` | decimal(15, 2) | 失败金额 · 可空 |
| `DIFFERENT_COUNT` | decimal | 差异笔数 · 可空 |
| `DIFFERENT_AMOUNT` | decimal(15, 2) | 差异金额 · 可空 |
| `LESS_COUNT` | decimal | 少账比数 · 可空 |
| `MORE_COUNT` | decimal | 多账比数 · 可空 |
| `STATUS` | char | 待补 |
| `FILE_PATH` | varchar(128) | 文件路径 · 可空 |
| `GMT_RETURN` | timestamp | 返回时间 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `FUND_CHANNEL_API` | varchar(32) | 资金渠道API · 可空 |
| `BIZ_TYPE` | char | 业务类型 · 可空 |
| `CHECK_OPERATER` | varchar(32) | 导入操作员的登录名 · 可空 |
| `IMPORT_OPERATER` | varchar(32) | 审核操作员的登录名 · 可空 |
| `IMPORT_TYPE` | char | 是否是第一次导入 F 第一次 S 第二次 · 可空 |

## 主键 / 索引
- 主键:`BATCH_RESULT_ID`
- `IX_TTINSTBATCHRESULT_BATCHID`:ARCHIVE_BATCH_ID

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
