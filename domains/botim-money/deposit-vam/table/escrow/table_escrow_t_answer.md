---
id: tbl_escrow_t_answer
object_type: Table
name: 银行回复详情表 (t_answer)
aliases: [t_answer, escrow.t_answer]
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

# 银行回复详情表 (t_answer)

## 用途
物理表 `escrow.t_answer`,主键 `id`。银行回复详情表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | id |
| `card_no` | varchar(32) | 卡号 |
| `bank_code` | varchar(32) | 银行编号，区分银行 |
| `answer_status` | varchar(4) | 状态，U-Unprocessed待处理, F-Fail处理失败, S-Success处理成功 |
| `answer_file_id` | varchar(32) | 响应文件编号 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 更新时间 · 可空 |
| `error_code` | varchar(32) | 错误码 · 可空 |
| `error_message` | varchar(512) | 错误映射 · 可空 |
| `resp_status` | varchar(4) | 响应状态,S-Success开卡成功,F-Fail开卡失败 |

## 主键 / 索引
- 主键:`id`
- `idx_bankCode_answerFile`:bank_code, answer_file_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
