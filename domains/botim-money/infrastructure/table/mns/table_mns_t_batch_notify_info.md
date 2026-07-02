---
id: tbl_mns_t_batch_notify_info
object_type: Table
name: t_batch_notify_info (t_batch_notify_info)
aliases: [t_batch_notify_info, mns.t_batch_notify_info]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mns schema DDL
tags: [infrastructure, mns]
sensitivity: normal
related_services: []
---

# t_batch_notify_info (t_batch_notify_info)

## 用途
物理表 `mns.t_batch_notify_info`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `file_name` | varchar(255) | 上传文件名 |
| `file_tag` | varchar(255) | ufs地址 |
| `status` | tinyint(2) | 0:初始化；1:处理中；2:处理完成 |
| `send_type` | varchar(2) | R:实时；T:定时 |
| `template_no` | varchar(50) | 模板ID · 可空 |
| `msg_content` | text | 消息内容信息 · 可空 |
| `subject` | varchar(256) | 主题信息 · 可空 |
| `ip_addr` | varchar(32) | 发送ip · 可空 |
| `send_time` | timestamp | 生效时间 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 |
| `create_by` | varchar(64) | 创建人 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `send_count` | int | 发送记录总条数 · 可空 |
| `succeed_count` | int | 成功条数 · 可空 |
| `failed_count` | int | 失败条数 · 可空 |
| `app_id` | varchar(20) | 发送appId |
| `account_from` | varchar(32) | ToTok公众号 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
