---
id: tbl_outman_tb_channel_api
object_type: Table
name: 渠道参数表 (tb_channel_api)
aliases: [tb_channel_api, outman.tb_channel_api]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: outman schema DDL
tags: [payment-core, outman]
sensitivity: normal
related_services: []
---

# 渠道参数表 (tb_channel_api)

## 用途
物理表 `outman.tb_channel_api`,主键 `CHANNEL_API_ID`。渠道参数表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CHANNEL_API_ID` | bigint(32) | 待补 |
| `CHANNEL_CODE` | varchar(48) | 渠道编号 |
| `PARAM_NAME` | varchar(64) | 参数名称 |
| `PARAM_VALUE` | varchar(2048) | 参数值 |
| `VALID` | char | 1:有效 0 无效 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 · 可空 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `EXTENSION` | varchar(256) | 扩展 · 可空 |

## 主键 / 索引
- 主键:`CHANNEL_API_ID`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
