---
id: tbl_basicrcdata_tr_member_device
object_type: Table
name: 用户设备信息 (tr_member_device)
aliases: [tr_member_device, basicrcdata.tr_member_device]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basicrcdata schema DDL
tags: [risk, basicrcdata]
sensitivity: normal
related_services: []
---

# 用户设备信息 (tr_member_device)

## 用途
物理表 `basicrcdata.tr_member_device`,主键 `ID`。用户设备信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | int(10) | 主键 · 可空 |
| `DEVICE_ID` | int(10) | 设备id |
| `MEMBER_ID` | varchar(32) | 用户id |
| `FINGER_MARK_KEY` | varchar(50) | 指纹支付秘钥 · 可空 |
| `FACE_MARK_KEY` | varchar(50) | 扫脸支付秘钥 · 可空 |
| `CERTIFICATE_FLAG` | varchar(3) | 是否安装数字证书 · 可空 |
| `GRANT_STATUS` | varchar(3) | 授权状态（1：授权 0：未授权） · 可空 |
| `APP_VERSION` | varchar(16) | 应用版本 · 可空 |
| `HOST_APP` | varchar(50) | SDK宿主 |
| `HOST_APP_VERSION` | varchar(16) | SDK宿主版本 · 可空 |
| `FIRST_LOGIN_TIME` | timestamp | 最早登录时间 · 可空 |
| `LAST_LOGIN_TIME` | timestamp | 最后登录时间 · 可空 |
| `CREATE_TIME` | timestamp | 创建时间 · 可空 |
| `MODIFY_TIME` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`ID`
- `UK_MEMBER_DEVICE_HOST`:MEMBER_ID, DEVICE_ID, HOST_APP (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
