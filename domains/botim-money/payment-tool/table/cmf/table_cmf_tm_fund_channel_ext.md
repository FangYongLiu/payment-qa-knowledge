---
id: tbl_cmf_tm_fund_channel_ext
object_type: Table
name: 资金渠道道特性 (tm_fund_channel_ext)
aliases: [tm_fund_channel_ext, cmf.tm_fund_channel_ext]
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

# 资金渠道道特性 (tm_fund_channel_ext)

## 用途
物理表 `cmf.tm_fund_channel_ext`,主键 `EXT_ID`。资金渠道道特性。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `EXT_ID` | int unsigned | 扩展ID · 可空 |
| `FUND_CHANNEL_CODE` | varchar(32) | 资金源编码 |
| `ATTR_KEY` | varchar(32) | 属性名 |
| `ATTR_VALUE` | varchar(2560) | 属性值 · 可空 |
| `ATTR_TYPE` | char | 属性类型：N（无特殊制定），F（流量） |
| `VALUE_TYPE` | varchar(32) | 值类型 · 可空 |
| `VALUE_SPLIT` | char | 值分隔符，针对有多选属性使用 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `ATTR_CODE_KEY` | varchar(32) | 属性字典标识 · 可空 |
| `API_CODE` | varchar(32) | api编码 · 可空 |
| `NEED_MATCH` | char | 是否需要满足VALUE指定 · 可空 |
| `MATCH_TYPE` | varchar(32) | 比较类型 · 可空 |
| `GROUP_ID` | varchar(8) | 组号 · 可空 |
| `GROUP_TYPE` | varchar(32) | 组类型(or 逻辑或) · 可空 |

## 主键 / 索引
- 主键:`EXT_ID`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
