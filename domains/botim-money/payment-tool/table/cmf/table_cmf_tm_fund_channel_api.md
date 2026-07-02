---
id: tbl_cmf_tm_fund_channel_api
object_type: Table
name: 资金渠道接口 (tm_fund_channel_api)
aliases: [tm_fund_channel_api, cmf.tm_fund_channel_api]
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

# 资金渠道接口 (tm_fund_channel_api)

## 用途
物理表 `cmf.tm_fund_channel_api`,主键 `API_CODE`。资金渠道接口。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `API_CODE` | varchar(48) | 接口代码 |
| `FUND_CHANNEL_CODE` | varchar(32) | 资金源编码 |
| `API_TYPE` | varchar(16) | 接口类型：SP（单笔支付），BP（批量支付），SQ（单笔查询），BQ（批量查询），SR（单笔退款），BR（批量退款） |
| `API_VERSION` | varchar(64) | 接口版本 · 可空 |
| `API_METHOD` | varchar(128) | 接口方法 |
| `API_URI` | varchar(128) | 接口URI · 可空 |
| `API_PRIORITY` | decimal(3) | 优先级 |
| `SECURE` | char | 是否需要密钥证书 · 可空 |
| `MAX_ITEM` | decimal | 最大笔数 · 可空 |
| `COMM_TITLE_TEMPLATE` | varchar(64) | 通信标题模板，可用作文件名模板 · 可空 |
| `COMM_CONTENT_TEMPLATE` | varchar(1024) | 通信内容模板 · 可空 |
| `CHECK_PARSE_SCRIPT` | text | 复核解析脚本 · 可空 |
| `RESULT_PARSE_SCRIPT` | text | 结果解析脚本 · 可空 |
| `NEED_CONFIRM` | char | 是否需要审核：Y（是）；N（否）； |
| `ENABLE` | char | 是否可用：Y（可用），N（不可用） |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `API_NO_MODE_ID` | decimal(11) | 订单号生成模式 · 可空 |
| `API_SECURITY_ID` | decimal(11) | 渠道接口签名，加密方式 · 可空 |
| `CONSUME_TIME` | decimal(5, 2) | 渠道耗时，单位小时 · 可空 |
| `FILE_TYPE` | varchar(8) | 文件类型txt，excel · 可空 |
| `FILE_PATH` | varchar(256) | excel文件模板路径 · 可空 |
| `API_NAME` | varchar(32) | API名称 · 可空 |
| `NEED_SYNC_GLIDE` | char | Y需要同步流水, N不需要同步流水 · 可空 |
| `EXTENSION` | varchar(256) | 扩展 · 可空 |

## 主键 / 索引
- 主键:`API_CODE`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
