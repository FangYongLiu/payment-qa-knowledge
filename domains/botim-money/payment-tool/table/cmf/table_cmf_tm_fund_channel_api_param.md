---
id: tbl_cmf_tm_fund_channel_api_param
object_type: Table
name: tm_fund_channel_api_param (tm_fund_channel_api_param)
aliases: [tm_fund_channel_api_param, cmf.tm_fund_channel_api_param]
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

# tm_fund_channel_api_param (tm_fund_channel_api_param)

## 用途
物理表 `cmf.tm_fund_channel_api_param`,主键 `PARAM_ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PARAM_ID` | int unsigned | 主键ID · 可空 |
| `API_CODE` | varchar(48) | 接口编码 · 可空 |
| `PARAM_NAME` | varchar(32) | 参数名称 · 可空 |
| `PARAM_CODE_KEY` | varchar(32) | 参数字典标识 · 可空 |
| `PARAM_DESC` | varchar(128) | 参数描述 · 可空 |
| `NULL_ABLE` | char | 是否需要校验 · 可空 |
| `ENABLE` | char | 是否使用 · 可空 |
| `IS_SAVE` | char | 是否需要保存数据 · 可空 |
| `IS_ORGIN` | char | 是否登录 · 可空 |
| `SCENE` | varchar(12) | IN,入;OUT,出 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 · 可空 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |
| `IS_CHANNEL_TRANS` | char | 该信息是否从渠道获取,如招行需要每天更新密钥信息 · 可空 |
| `TRANS_CODE` | varchar(16) | 是用哪个交互编码查询到的数据 · 可空 |
| `EXTENSION` | varchar(512) | 扩展信息 · 可空 |

## 主键 / 索引
- 主键:`PARAM_ID`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
