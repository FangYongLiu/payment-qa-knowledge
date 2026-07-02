---
id: tbl_protocol_t_user_device_info
object_type: Table
name: 设备信息表 (t_user_device_info)
aliases: [t_user_device_info, protocol.t_user_device_info]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: protocol schema DDL
tags: [wallet, protocol]
sensitivity: normal
related_services: []
---

# 设备信息表 (t_user_device_info)

## 用途
物理表 `protocol.t_user_device_info`,主键 `ID`。设备信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint | 主键 · 可空 |
| `SIGN_INFO_ID` | bigint | 签约的协议ID · 可空 |
| `INFO_TYPE` | varchar(25) | 类型 |
| `DEVICE_MODEL` | varchar(100) | 设备型号 · 可空 |
| `SYSTEM` | varchar(50) | IOS/Android/Other |
| `SYSTEM_VERSION` | varchar(16) | 操作系统版本 · 可空 |
| `UUID` | varchar(50) | uuid · 可空 |
| `ROOT_FLAG` | varchar(1) | 是否开通ROOT权限 · 可空 |
| `APP_VERSION` | varchar(16) | 应用版本 · 可空 |
| `HOST_APP` | varchar(50) | SDK宿主 |
| `HOST_APP_VERSION` | varchar(16) | SDK宿主版本 · 可空 |
| `EXTENTION` | varchar(512) | 最后连接时间 · 可空 |
| `CREATE_TIME` | timestamp | 创建时间 |
| `UPDATE_TIME` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`ID`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
