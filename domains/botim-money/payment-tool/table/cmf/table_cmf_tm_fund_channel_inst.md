---
id: tbl_cmf_tm_fund_channel_inst
object_type: Table
name: 提供资金渠道的机构 (tm_fund_channel_inst)
aliases: [tm_fund_channel_inst, cmf.tm_fund_channel_inst]
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

# 提供资金渠道的机构 (tm_fund_channel_inst)

## 用途
物理表 `cmf.tm_fund_channel_inst`,主键 `INST_CODE`。提供资金渠道的机构。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `INST_CODE` | varchar(16) | 机构代码 |
| `INST_TYPE` | varchar(8) | 机构类型：BANK（银行），EPAY（电子支付公司） |
| `INST_NAME` | varchar(32) | 机构名称 |
| `INST_BRANCH_NAME` | varchar(64) | 机构分支名称 · 可空 |
| `BANK_LINE_NO` | varchar(32) | 联行号 · 可空 |
| `AREA_CODE` | varchar(16) | 地区 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `EXTENSION` | varchar(1024) | 扩展 · 可空 |

## 主键 / 索引
- 主键:`INST_CODE`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
