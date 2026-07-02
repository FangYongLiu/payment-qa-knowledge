---
id: tbl_basis_t_ues_decryption_auth_config
object_type: Table
name: ues解密权限表 (t_ues_decryption_auth_config)
aliases: [t_ues_decryption_auth_config, basis.t_ues_decryption_auth_config]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basis schema DDL
tags: [merchant-management, basis]
sensitivity: normal
related_services: []
---

# ues解密权限表 (t_ues_decryption_auth_config)

## 用途
物理表 `basis.t_ues_decryption_auth_config`,主键 `config_id`。ues解密权限表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | int | config id · 可空 |
| `permission` | varchar(32) | permission |
| `client_id` | varchar(32) | client id |
| `ues_data_type` | varchar(32) | ues data type |
| `enable_flag` | char | enable flag |
| `memo` | varchar(255) | memo · 可空 |
| `extension` | varchar(255) | extension · 可空 |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`config_id`
- `uk_permission_clientId_type`:permission, client_id, ues_data_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
