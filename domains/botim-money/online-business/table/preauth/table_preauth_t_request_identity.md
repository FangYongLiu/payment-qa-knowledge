---
id: tbl_preauth_t_request_identity
object_type: Table
name: 请求标识 (t_request_identity)
aliases: [t_request_identity, preauth.t_request_identity]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: preauth schema DDL
tags: [online-business, preauth]
sensitivity: normal
related_services: []
---

# 请求标识 (t_request_identity)

## 用途
物理表 `preauth.t_request_identity`,主键 `global_id`。请求标识。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 退款全局号 |
| `issuer_type` | varchar(50) | 发起人类型 |
| `issuer_code` | varchar(200) | 发起人代码 |
| `request_no` | varchar(200) | 商户订单号 |
| `voucher_type` | varchar(32) | 凭证类型 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`global_id`
- `i_ri_no`:request_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
