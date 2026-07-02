---
id: tbl_pfs_tb_message_05
object_type: Table
name: 增长，10000行/天，至少保留三个月 (tb_message_05)
aliases: [tb_message_05, pfs.tb_message_05]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pfs schema DDL
tags: [payment-core, pfs]
sensitivity: normal
related_services: []
---

# 增长，10000行/天，至少保留三个月 (tb_message_05)

## 用途
物理表 `pfs.tb_message_05`,主键 `MESSAGE_ID`。增长，10000行/天，至少保留三个月。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `MESSAGE_ID` | decimal(18) | 消息Id |
| `CONFIG_ID` | decimal(15) | 消息配置Id |
| `MESSAGE_KEY` | varchar(256) | 消息标识 |
| `MESSAGE_TYPE` | varchar(128) | 消息类型 |
| `MESSAGE_CONTENT` | varchar(4000) | 消息内容 |
| `NOTIFY_TARGET` | varchar(128) | 通知目标 |
| `GMT_ALLOW` | timestamp | 允许通知时间 |
| `NOTIFY_COUNT` | decimal(8) | 已通知次数 |
| `NOTIFY_STATUS` | char | 通知状态：S成功，F失败，I初始 |
| `LAST_NOTIFY_LOG` | varchar(256) | 最近通知日志 |
| `MARKER` | varchar(64) | 标记者 |
| `EXTENSIONS` | varchar(512) | 扩展信息 · 可空 |
| `OPERATOR` | varchar(32) | 操作员 |
| `LAST_NOTIFIER` | varchar(64) | 最近发送方 · 可空 |
| `GMT_LAST_NOTIFY` | timestamp | 最近通知时间 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`MESSAGE_ID`
- `I_MESSAGE_GMTALLOW_05`:GMT_ALLOW
- `I_MESSAGE_GMTMODIFY_05`:GMT_MODIFY
- `I_MESSAGE_MESSAGEKEY_05`:MESSAGE_KEY

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
