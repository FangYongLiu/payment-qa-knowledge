---
id: tbl_cmf_tl_monitor_log
object_type: Table
name: 监控日志 (tl_monitor_log)
aliases: [tl_monitor_log, cmf.tl_monitor_log]
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

# 监控日志 (tl_monitor_log)

## 用途
物理表 `cmf.tl_monitor_log`,主键 `LOG_ID`。监控日志。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `LOG_ID` | decimal(11) | 日志ID |
| `IP_ADDRESS` | varchar(32) | IP地址 · 可空 |
| `ORDER_NO` | varchar(32) | 订单号 · 可空 |
| `EVENT_MESSAGE` | varchar(256) | 事件描述 · 可空 |
| `ACTION_ID` | varchar(32) | 监控事件ID |
| `ALERT_LEVEL` | varchar(16) | 报警级别: info, warn, error, fatal |
| `LOG_STATUS` | char | log状态 |
| `EXCEPTION_LOG` | varchar(2000) | 异常日志 · 可空 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |

## 主键 / 索引
- 主键:`LOG_ID`
- `IDX_TL_MONITOR_LOG_GT`:GMT_CREATE

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
