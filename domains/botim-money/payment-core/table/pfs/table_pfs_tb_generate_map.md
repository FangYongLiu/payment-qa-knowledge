---
id: tbl_pfs_tb_generate_map
object_type: Table
name: 生成匹配配置，稳定，100行 (tb_generate_map)
aliases: [tb_generate_map, pfs.tb_generate_map]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pfs schema DDL
tags: [payment-core, pfs]
sensitivity: normal
related_services: []
---

# 生成匹配配置，稳定，100行 (tb_generate_map)

## 用途
物理表 `pfs.tb_generate_map`,主键 `MAP_ID`。生成匹配配置，稳定，100行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `MAP_ID` | bigint | 匹配Id · 可空 |
| `MAP_CODE` | varchar(32) | 匹配配置唯一标识 |
| `MATCH_PRODUCT_CODE` | varchar(32) | 匹配产品编码 |
| `MATCH_BIZ_TYPE` | varchar(32) | 匹配业务类型 |
| `MATCH_EXPRESSION` | varchar(2000) | 匹配表达式 |
| `DEFAULT_FLAG` | char | 默认标识 |
| `PAYMENT_CODE` | varchar(16) | 支付编码 |
| `GEN_GROUP_CODE` | varchar(32) | 生成集编码 |
| `MEMO` | varchar(512) | 备注 · 可空 |
| `ENABLE_FLAG` | char | Y=有效，N=无效 |
| `GMT_VALID` | timestamp | 生效时间 |
| `GMT_EXPIRE` | timestamp | 过期时间 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`MAP_ID`
- `UK_GENERATE_MAP_MAPCODE`:MAP_CODE (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
