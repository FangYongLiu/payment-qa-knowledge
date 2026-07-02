---
id: tbl_escrow_t_inst_communication_record
object_type: Table
name: 机构通信表 (t_inst_communication_record)
aliases: [t_inst_communication_record, escrow.t_inst_communication_record]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 机构通信表 (t_inst_communication_record)

## 用途
物理表 `escrow.t_inst_communication_record`,主键 `id`。机构通信表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | 主键id |
| `member_id` | varchar(16) | 会员id |
| `card_id` | varchar(16) | 虚拟卡id |
| `api_type` | varchar(32) | api类型 |
| `communication_status` | varchar(1) | 通信状态, I-初始,P-上报中,S-成功,R-Retry · 可空 |
| `request_data` | varchar(1024) | 请求详情 |
| `response_data` | varchar(1024) | 响应详情 |
| `retry_time` | int(5) | 重试次数 · 可空 |
| `gmt_create` | timestamp(6) | 创建时间 |
| `gmt_modified` | timestamp(6) | 修改时间 · 可空 |
| `memo` | varchar(64) | 备注 · 可空 |
| `channel_resp_code` | varchar(32) | 银行响应码 · 可空 |
| `channel_resp_message` | varchar(128) | 银行响应描述 · 可空 |
| `gmt_retry_trigger` | timestamp | 触发时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_gmt_create`:gmt_create, communication_status
- `idx_memberId_cardId`:member_id, card_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
