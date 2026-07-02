---
id: tbl_outman_tb_channel
object_type: Table
name: 渠道信息表 (tb_channel)
aliases: [tb_channel, outman.tb_channel]
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

# 渠道信息表 (tb_channel)

## 用途
物理表 `outman.tb_channel`,主键 `CHANNEL_ID`。渠道信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CHANNEL_ID` | bigint(32) | 渠道编号 |
| `CHANNEL_CODE` | varchar(32) | 渠道编码 |
| `CHANNEL_NAME` | varchar(64) | 渠道名称 |
| `BIZ_TYPE` | varchar(64) | 业务类型,(CERTVSMSMAIL) |
| `TAG` | varchar(256) | 标签:用于详细标记该渠道的特征 · 可空 |
| `VALID` | char | 1:有效 0 无效 |
| `MEMO` | varchar(256) | memo · 可空 |
| `GMT_MAINTAIN_PERIOD` | varchar(4000) | 维护期:标记该渠道该段时间不可用 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`CHANNEL_ID`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
