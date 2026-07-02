---
id: tbl_pfs_tb_generate
object_type: Table
name: 生成配置，稳定，100行 (tb_generate)
aliases: [tb_generate, pfs.tb_generate]
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

# 生成配置，稳定，100行 (tb_generate)

## 用途
物理表 `pfs.tb_generate`,主键 `GEN_ID`。生成配置，稳定，100行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `GEN_ID` | bigint | 配置Id · 可空 |
| `GEN_GROUP_CODE` | varchar(32) | 生成集编码 |
| `GEN_CODE` | varchar(32) | 生成编码 |
| `PAYMENT_TYPE` | varchar(10) | 支付类型 |
| `GEN_PRIORITY` | decimal(8) | 优先级 · 可空 |
| `PAYMENT_SERVICE_CODE` | varchar(16) | 支付服务 · 可空 |
| `FAILURE_ACTION` | varchar(32) | 失败动作 · 可空 |
| `EXTENSIONS` | varchar(1000) | 扩展信息 · 可空 |
| `MEMO` | varchar(512) | 备注 · 可空 |
| `ENABLE_FLAG` | char | 生效标识：Y=生效，N=不生效 |
| `GMT_VALID` | timestamp | 生效时间 |
| `GMT_EXPIRE` | timestamp | 过期时间 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`GEN_ID`
- `UK_GENERATE_GROUP_GENCODE`:GEN_GROUP_CODE, GEN_CODE (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
