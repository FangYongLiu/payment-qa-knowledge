---
id: tbl_upic_t_key_config
object_type: Table
name: 密钥配置 (t_key_config)
aliases: [t_key_config, upic.t_key_config]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: upic schema DDL
tags: [card, upic]
sensitivity: normal
related_services: []
---

# 密钥配置 (t_key_config)

## 用途
物理表 `upic.t_key_config`,主键 `config_id`。密钥配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | bigint | 配置ID · 可空 |
| `kid` | bigint | kid |
| `role_code` | varchar(10) | 角色：APP, ISSUER |
| `generator` | varchar(10) | 生成者：UPI, INST |
| `purpose` | varchar(10) | 密钥用途：SIGN=签名，验签；ENCRYPT=加密，解密 |
| `key_status` | varchar(10) | 密钥状态：A=可用，D=不可用，P=处理中，E=失效中 |
| `valid_time` | timestamp | 生效时间 |
| `expire_time` | timestamp | 失效时间 |
| `schedule_update_time` | timestamp | 计划更新时间 · 可空 |
| `private_key` | varchar(1024) | 私钥 · 可空 |
| `cert_content` | varchar(4000) | 证书内容 · 可空 |
| `old_config_id` | bigint | 老密钥ID · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`config_id`
- `uk_biz_key`:kid, role_code, generator, purpose (UNIQUE)
- `idx_schedule_update_time`:schedule_update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
