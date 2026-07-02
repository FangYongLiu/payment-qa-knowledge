---
id: tbl_pcm_t_pcm_bind_token_map
object_type: Table
name: 付款码绑定信息表 (t_pcm_bind_token_map)
aliases: [t_pcm_bind_token_map, pcm.t_pcm_bind_token_map]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pcm schema DDL
tags: [payment-core, pcm]
sensitivity: normal
related_services: []
---

# 付款码绑定信息表 (t_pcm_bind_token_map)

## 用途
物理表 `pcm.t_pcm_bind_token_map`,主键 `ID`。付款码绑定信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint(17) | 主键 |
| `MEMBER_ID` | varchar(50) | 会员ID |
| `DEVICE_ID` | varchar(255) | 设备指纹 |
| `HOST_APP` | varchar(50) | 宿主应用 |
| `EXPIRE_TIME` | timestamp | 失效日期 |
| `PTOKEN` | varchar(255) | 加密密钥 |
| `STATUS` | tinyint | 状态：0 关闭  1 启用 2 失效 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`ID`
- `idx_t_pcm_bind_token_map_memberid`:MEMBER_ID

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
