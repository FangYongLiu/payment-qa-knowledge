---
id: tbl_npss_t_issue_log
object_type: Table
name: 问题日志 (t_issue_log)
aliases: [t_issue_log, npss.t_issue_log]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# 问题日志 (t_issue_log)

## 用途
物理表 `npss.t_issue_log`,主键 `log_id`。问题日志。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `log_id` | bigint(17) | 日志id |
| `issue_log_type` | varchar(6) | 问题日志类型，ENROLL-注册，UPDATE-更新 |
| `member_id` | varchar(20) | 会员id |
| `mobile_no` | varchar(20) | 手机号 · 可空 |
| `eid` | varchar(20) | 身份证号 · 可空 |
| `extension` | varchar(1024) | 扩展参数 · 可空 |
| `request_id` | varchar(32) | 请求id · 可空 |
| `gmt_request` | timestamp | 请求时间 |
| `response_code` | varchar(32) | 响应结果码 · 可空 |
| `response_msg` | varchar(128) | 响应备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`log_id`
- `idx_issue_log_gmt_crt`:gmt_create

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
