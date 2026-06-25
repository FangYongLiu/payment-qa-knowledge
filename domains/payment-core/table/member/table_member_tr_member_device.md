---
id: tbl_member_tr_member_device
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- device
- tr_member_device
subdomain: device
module: null
sensitivity: restricted
name: 用户设备信息(tr_member_device)
aliases:
- tr_member_device
related_services:
- svc_member
related_scenarios: []
---

# 用户设备信息(tr_member_device)

## 用途
用户设备信息。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | int(10) | PK | 主键 |
| `DEVICE_ID` | int(10) | NOT NULL | 设备id |
| `MEMBER_ID` | varchar(32) | NOT NULL | 用户id |
| `FINGER_MARK_KEY` | varchar(50) | 默认 '' | 指纹支付秘钥 |
| `FACE_MARK_KEY` | varchar(50) | 默认 '' | 扫脸支付秘钥 |
| `CERTIFICATE_FLAG` | varchar(3) | 默认 '' | 是否安装数字证书 |
| `GRANT_STATUS` | varchar(3) | 默认 '' | 授权状态（1：授权 0：未授权） |
| `APP_VERSION` | varchar(16) | 默认 '' | 应用版本 |
| `HOST_APP` | varchar(50) | NOT NULL | SDK宿主 |
| `FIRST_LOGIN_TIME` | timestamp |  | 最早登录时间 |
| `LAST_LOGIN_TIME` | timestamp |  | 最后登录时间 |
| `CREATE_TIME` | timestamp |  | 创建时间 |
| `MODIFY_TIME` | timestamp |  | 修改时间 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
