---
id: tbl_protocol_t_contract_package
object_type: Table
name: 协议包 (t_contract_package)
aliases: [t_contract_package, protocol.t_contract_package]
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

# 协议包 (t_contract_package)

## 用途
物理表 `protocol.t_contract_package`,主键 `id`。协议包。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `package_code` | varchar(25) | 协议包code |
| `package_name` | varchar(35) | 协议包名称 |
| `package_type` | varchar(25) | 包类型 如：支付授权协议，登陆协议 |
| `status` | varchar(5) | 状态 Y：有效，N：无效 |
| `extension` | varchar(512) | 拓展字段 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `memo` | varchar(255) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
