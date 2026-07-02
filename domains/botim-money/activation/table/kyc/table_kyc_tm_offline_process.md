---
id: tbl_kyc_tm_offline_process
object_type: Table
name: 线下处理登记表 用来记录线程处理的业务流程 (tm_offline_process)
aliases: [tm_offline_process, kyc.tm_offline_process]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: kyc schema DDL
tags: [activation, kyc]
sensitivity: normal
related_services: []
---

# 线下处理登记表 用来记录线程处理的业务流程 (tm_offline_process)

## 用途
物理表 `kyc.tm_offline_process`,主键 `id`。线下处理登记表 用来记录线程处理的业务流程。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `member_id` | varchar(32) | 会员ID · 可空 |
| `biz_type` | int | 业务类型 · 可空 |
| `biz_record_id` | bigint | 业务记录表 · 可空 |
| `notice_type` | varchar(32) | 通知类型 1-邮件；2-短信； · 可空 |
| `notice_count` | int | 通知次数 · 可空 |
| `status` | varchar(32) | 当前状态 0-初始化（处理中）；1-已处理 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
