---
id: tbl_device_t_pos_menu
object_type: Table
name: POS菜单资源 (t_pos_menu)
aliases: [t_pos_menu, device.t_pos_menu]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: device schema DDL
tags: [offline-business, device]
sensitivity: normal
related_services: []
---

# POS菜单资源 (t_pos_menu)

## 用途
物理表 `device.t_pos_menu`,主键 `id`。POS菜单资源。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `name` | varchar(50) | 名称 |
| `code` | varchar(50) | 编码 |
| `need_pwd` | varchar(3) | 是否需要密码 |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `merchant_mid` | varchar(32) | 商户id · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_mid_code`:merchant_mid, code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
