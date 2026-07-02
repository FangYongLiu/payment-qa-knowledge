---
id: tbl_autodebit_t_ca_config
object_type: Table
name: autodebit (t_ca_config)
aliases: [t_ca_config, autodebit.t_ca_config]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: autodebit schema DDL
tags: [wallet, autodebit]
sensitivity: normal
related_services: []
---

# autodebit (t_ca_config)

## 用途
物理表 `autodebit.t_ca_config`,主键 `id`。autodebit。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `status` | varchar(20) | 待补 |
| `private_key` | varchar(2000) | 私钥 · 可空 |
| `public_key` | varchar(2000) | 公钥 · 可空 |
| `product_code` | varchar(20) | 产品 · 可空 |
| `partner_id` | varchar(20) | 签约商户号 · 可空 |
| `ext` | varchar(255) | 额外信息 · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
