---
id: tbl_protocol_t_sign_apply_request
object_type: Table
name: 申请协议请求记录表 (t_sign_apply_request)
aliases: [t_sign_apply_request, protocol.t_sign_apply_request]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: protocol schema DDL
tags: [wallet, protocol]
sensitivity: normal
related_services: []
---

# 申请协议请求记录表 (t_sign_apply_request)

## 用途
物理表 `protocol.t_sign_apply_request`,主键 `voucher_no`。申请协议请求记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `voucher_no` | bigint | 协议申请凭证号 |
| `request_no` | varchar(35) | 请求编号 |
| `lang_type` | varchar(15) | 语言 |
| `scenes` | varchar(25) | 场景 · 可空 |
| `user_id` | varchar(64) | User ID · 可空 |
| `merchant_id` | varchar(25) | 商户ID · 可空 |
| `merchant_name` | varchar(255) | 商户名称 · 可空 |
| `partner_id` | varchar(25) | 平台ID · 可空 |
| `expired_time` | datetime | 过期时间，单位分钟，如15 · 可空 |
| `source_id` | varchar(25) | 申请来源 · 可空 |
| `close_time` | timestamp | 关闭时间 · 可空 |
| `reject_time` | timestamp | 拒绝时间 · 可空 |
| `status` | varchar(25) | 状态 · 可空 |
| `extension` | varchar(512) | 拓展参数 · 可空 |
| `fail_code` | varchar(25) | 失败错误码 · 可空 |
| `fail_message` | varchar(255) | 失败错误描述 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`voucher_no`
- `idx_created_time`:create_time
- `idx_expiry`:expired_time, status
- `idx_request_no`:request_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
