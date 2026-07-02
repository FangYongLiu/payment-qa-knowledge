---
id: tbl_ccdeposit_t_customer_deposit_notify_url
object_type: Table
name: 客户充值URL配置 (t_customer_deposit_notify_url)
aliases: [t_customer_deposit_notify_url, ccdeposit.t_customer_deposit_notify_url]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccdeposit schema DDL
tags: [crypto, ccdeposit]
sensitivity: normal
related_services: []
---

# 客户充值URL配置 (t_customer_deposit_notify_url)

## 用途
物理表 `ccdeposit.t_customer_deposit_notify_url`,主键 `id`。客户充值URL配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `notification_url` | varchar(128) | 通知地址 |
| `member_id` | varchar(32) | 用户MID |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `uk_cdnu_mem`:member_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
