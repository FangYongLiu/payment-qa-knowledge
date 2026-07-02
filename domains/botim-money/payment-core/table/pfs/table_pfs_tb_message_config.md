---
id: tbl_pfs_tb_message_config
object_type: Table
name: 稳定，100行 (tb_message_config)
aliases: [tb_message_config, pfs.tb_message_config]
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

# 稳定，100行 (tb_message_config)

## 用途
物理表 `pfs.tb_message_config`,主键 `CONFIG_ID`。稳定，100行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CONFIG_ID` | decimal(15) | 配置Id |
| `CONFIG_NAME` | varchar(256) | 配??名称 |
| `EVENT_CODE_ID` | decimal(15) | 事件编码Id |
| `MATCH_EXPRESSION` | varchar(2000) | 配置匹配表达式 · 可空 |
| `COLLECTOR_TYPE` | varchar(64) | 内容采集类型 |
| `NOTIFY_TARGET` | varchar(256) | 通知目标 |
| `EXTENSIONS` | varchar(2000) | 扩展信息 · 可空 |
| `ENABLE_FLAG` | char | 启用标识：Y启用，N停用 |
| `GMT_VALID` | timestamp | 生效时间 |
| `GMT_EXPIRE` | timestamp | 失效时间 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `OPERATOR` | varchar(128) | 操作员 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`CONFIG_ID`
- `UK_MESSAGE_CONFIG_CONFIGNAME`:CONFIG_NAME (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
