---
id: tbl_cmf_tm_event_notify_config
object_type: Table
name: 配置通知的事件,包括通知地址,最大通知次数等 (tm_event_notify_config)
aliases: [tm_event_notify_config, cmf.tm_event_notify_config]
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

# 配置通知的事件,包括通知地址,最大通知次数等 (tm_event_notify_config)

## 用途
物理表 `cmf.tm_event_notify_config`,主键 `NOTIFY_CONFIG_ID`。配置通知的事件,包括通知地址,最大通知次数等。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `NOTIFY_CONFIG_ID` | decimal(11) | 通知配置ID |
| `EVENT` | char(2) | 事件 |
| `PROTOCOL` | varchar(10) | MQ-MQ协议, MQ_T- MQ TOPIC方式,HTTP-HTTP回调 |
| `TARGET_ADDRESS` | varchar(200) | HTTP协议: URI MQ协议:MQNAME |
| `CONDITION` | varchar(200) | 发送条件,暂未实现 · 可空 |
| `MAX_RETRY_TIMES` | decimal(2) | 最大重试时间 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `ENABLE` | char | 是否可用：Y（可用）,N（不可用） |

## 主键 / 索引
- 主键:`NOTIFY_CONFIG_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
