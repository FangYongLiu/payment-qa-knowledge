---
id: tbl_acs_t_key_config_1706515200000
object_type: Table
name: 密钥配置 (t_key_config_1706515200000)
aliases: [t_key_config_1706515200000, acs.t_key_config_1706515200000]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acs schema DDL
tags: [risk, acs]
sensitivity: normal
related_services: []
---

# 密钥配置 (t_key_config_1706515200000)

## 用途
物理表 `acs.t_key_config_1706515200000`,主键 `CONFIG_ID`。密钥配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CONFIG_ID` | bigint | 配置ID · 可空 |
| `GATEWAY_TYPE` | varchar(10) | 网关类型：CGS=客户端网关，SGS=服务端网关 |
| `PARTNER_ID` | varchar(20) | 合作方ID |
| `ALGORITHM` | varchar(20) | 算法，RSA等 |
| `CERT_TYPE` | varchar(10) | 密钥类型：PRIVATE=签名解密，PUBLIC=验签加密 |
| `CERT` | text | 密钥 |
| `RELATE_CERT` | varchar(4000) | 关联密钥，比如：公钥 · 可空 |
| `GMT_EFFECT` | timestamp | 生效时间 |
| `GMT_EXPIRED` | timestamp | 失效时间 |
| `ENABLE_FLAG` | char | 状态：Y=启用，N=停用 |
| `EXTENSION` | varchar(200) | 扩展参数 · 可空 |
| `MEMO` | varchar(200) | 备注 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`CONFIG_ID`
- `I_KEY_CONFIG_PARTNER_ID`:PARTNER_ID

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
