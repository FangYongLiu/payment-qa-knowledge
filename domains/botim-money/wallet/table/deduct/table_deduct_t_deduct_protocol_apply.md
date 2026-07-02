---
id: tbl_deduct_t_deduct_protocol_apply
object_type: Table
name: Deduct Protocol Application (t_deduct_protocol_apply)
aliases: [t_deduct_protocol_apply, deduct.t_deduct_protocol_apply]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: deduct schema DDL
tags: [wallet, deduct]
sensitivity: normal
related_services: []
---

# Deduct Protocol Application (t_deduct_protocol_apply)

## 用途
物理表 `deduct.t_deduct_protocol_apply`,主键 `id`。Deduct Protocol Application。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Apply ID;ID, 前8后9 |
| `apply_request_no` | bigint | Apply Request No;Voucher No |
| `sign_type` | char | Sign Type;T=Sign after Trade |
| `merchant_id` | varchar(20) | Merchant ID |
| `partner_id` | varchar(20) | Partner ID |
| `merchant_request_no` | varchar(64) | Merchant Request No |
| `protocol_scene_code` | char(3) | Protocol Scene Code · 可空 |
| `internal_partner_flag` | char | Internal Partner Flag;Y=Yes, N=No |
| `status` | char | Status;A=Applying, C=Closed, F=Failure, S=Signed |
| `trade_request_no` | bigint | Trade Request No · 可空 |
| `notify_url` | varchar(200) | Notify Url · 可空 |
| `deduct_protocol_no` | bigint | Deduct Protocol No · 可空 |
| `unity_result_code` | varchar(50) | Unity Result Code · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp(3) | Create Time |
| `update_time` | timestamp(3) | Update Time |

## 主键 / 索引
- 主键:`id`
- `uk_apply_request_no`:apply_request_no (UNIQUE)
- `idx_deduct_protocol_no`:deduct_protocol_no
- `idx_trade_request_no`:trade_request_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
