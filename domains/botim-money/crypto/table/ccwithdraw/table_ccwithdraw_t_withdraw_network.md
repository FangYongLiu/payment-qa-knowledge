---
id: tbl_ccwithdraw_t_withdraw_network
object_type: Table
name: 提现网络配置 (t_withdraw_network)
aliases: [t_withdraw_network, ccwithdraw.t_withdraw_network]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccwithdraw schema DDL
tags: [crypto, ccwithdraw]
sensitivity: normal
related_services: []
---

# 提现网络配置 (t_withdraw_network)

## 用途
物理表 `ccwithdraw.t_withdraw_network`,主键 `asset_code, network`。提现网络配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `asset_code` | varchar(32) | 币种 |
| `network` | varchar(32) | 待补 |

## 主键 / 索引
- 主键:`asset_code, network`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
