---
id: tbl_contract_t_expire_contract
object_type: Table
name: 无效协议 (t_expire_contract)
aliases: [t_expire_contract, contract.t_expire_contract]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: contract schema DDL
tags: [merchant-management, contract]
sensitivity: normal
related_services: []
---

# 无效协议 (t_expire_contract)

## 用途
物理表 `contract.t_expire_contract`,主键 `id`。无效协议。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `contract_no` | bigint | 协议编号 |
| `product_code` | varchar(32) | 产品编码 |
| `merchant_mid` | varchar(32) | 商户id |
| `operate_behavior` | varchar(32) | 协议操作行为 |
| `file_path` | varchar(300) | 文件路径 · 可空 |
| `effect_time` | timestamp | 生效时间 · 可空 |
| `expire_time` | timestamp | 失效时间 · 可空 |
| `first_party_mid` | varchar(32) | 甲方Mid · 可空 |
| `second_party_mid` | varchar(32) | 乙方Mid · 可空 |
| `created_time` | timestamp | 创建时间 |
| `contract_version` | varchar(10) |  · 可空 |
| `ip_address` | varchar(40) | IP · 可空 |
| `browser` | varchar(10) |  · 可空 |
| `device_id` | varchar(30) | ID · 可空 |
| `acceptance_time` | timestamp |  · 可空 |
| `merchant_email` | varchar(100) | 商户注册邮箱 · 可空 |
| `activity_log` | varchar(300) |  · 可空 |
| `mobile` | varchar(20) | 签约手机号 · 可空 |
| `login_time` | timestamp | 签约登录时间 · 可空 |
| `login_type` | char(3) | 登录类型： · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
