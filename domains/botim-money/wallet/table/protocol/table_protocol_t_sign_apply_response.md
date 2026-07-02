---
id: tbl_protocol_t_sign_apply_response
object_type: Table
name: 申请协议请求记录表 (t_sign_apply_response)
aliases: [t_sign_apply_response, protocol.t_sign_apply_response]
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

# 申请协议请求记录表 (t_sign_apply_response)

## 用途
物理表 `protocol.t_sign_apply_response`,主键 `id`。申请协议请求记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `voucher_no` | bigint(25) | 协议申请凭证号 |
| `package_id` | bigint | 包ID · 可空 |
| `contract_no` | varchar(25) | 协议模版编号 · 可空 |
| `contract_version` | varchar(25) | 协议版本号 · 可空 |
| `contract_type` | varchar(35) | 协议大类型 · 可空 |
| `contract_sub_type` | varchar(35) | 协议子类型 · 可空 |
| `url` | varchar(1024) | 协议内容url · 可空 |
| `merchant_id` | varchar(25) | 商户ID · 可空 |
| `merchant_name` | varchar(255) | 商户名称 · 可空 |
| `user_id` | varchar(64) | User ID · 可空 |
| `title` | varchar(255) | 协议标题 · 可空 |
| `summary` | varchar(1024) | 协议描述 · 可空 |
| `extension` | varchar(512) | 拓展参数 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `i_sas_voucher_no`:voucher_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
