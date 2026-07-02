---
id: tbl_ppc_t_key_config
object_type: Table
name: Key Config (t_key_config)
aliases: [t_key_config, ppc.t_key_config]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Key Config (t_key_config)

## 用途
物理表 `ppc.t_key_config`,主键 `key_id`。Key Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `key_id` | bigint | Key Id · 可空 |
| `purpose_code` | varchar(32) | Purpose Code: TAV_SK=TAV Secret Key, PEPK=Payload Encryption Public Key |
| `key_path` | varchar(200) | Key Path |
| `enable_flag` | char | Enable Flag: Y=Yes, N=No |
| `priority` | int | Priority |
| `key_alias` | varchar(32) | Key Alias · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `valid_time` | timestamp | Valid Time |
| `expiry_time` | timestamp | Expiry Time |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`key_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
