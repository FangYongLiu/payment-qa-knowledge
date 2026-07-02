---
id: tbl_payment_tb_generate_group
object_type: Table
name: 生成集，稳定，100行 (tb_generate_group)
aliases: [tb_generate_group, payment.tb_generate_group]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: payment schema DDL
tags: [payment-core, payment]
sensitivity: normal
related_services: []
---

# 生成集，稳定，100行 (tb_generate_group)

## 用途
物理表 `payment.tb_generate_group`,主键 `GEN_GROUP_CODE`。生成集，稳定，100行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `GEN_GROUP_CODE` | varchar(32) | 生成集编码 |
| `STATE_MACHINE_CODE` | varchar(32) | 状态机编码 |
| `EXTENSIONS` | varchar(1000) | 扩展信息 · 可空 |
| `MEMO` | varchar(512) | 备注 · 可空 |
| `ENABLE_FLAG` | char | 生效标识：Y=生效，N=不生效 |
| `GMT_VALID` | timestamp | 生效时间 |
| `GMT_EXPIRE` | timestamp | 过期时间 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`GEN_GROUP_CODE`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
