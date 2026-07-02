---
id: tbl_cmf_tm_fund_channel_target_inst
object_type: Table
name: tm_fund_channel_target_inst (tm_fund_channel_target_inst)
aliases: [tm_fund_channel_target_inst, cmf.tm_fund_channel_target_inst]
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

# tm_fund_channel_target_inst (tm_fund_channel_target_inst)

## 用途
物理表 `cmf.tm_fund_channel_target_inst`,主键 `TARGET_INST_CODE`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `TARGET_INST_CODE` | varchar(16) | 目标机构代码 |
| `SHORT_NAME` | varchar(20) | 简称 |
| `TARGET_INST_NAME` | varchar(50) | 目标机构名称 |
| `TARGET_INST_DESC` | varchar(256) | 目标机构排序 · 可空 |
| `ICON_URL` | varchar(256) | 图标地址 · 可空 |
| `AMOUNT_LIMIT_DESC` | text | 金额限制排序 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 · 可空 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`TARGET_INST_CODE`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
