---
id: tbl_escrow_t_issue_record
object_type: Table
name: kyc报备信息表 (t_issue_record)
aliases: [t_issue_record, escrow.t_issue_record]
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

# kyc报备信息表 (t_issue_record)

## 用途
物理表 `escrow.t_issue_record`,主键 `id`。kyc报备信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | id |
| `card_no` | varchar(32) | 银行卡编号 · 可空 |
| `card_id` | varchar(32) | 虚拟卡编号 · 可空 |
| `member_id` | varchar(32) | 会员编号 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 更新时间 · 可空 |
| `name` | varchar(255) | 姓名 |
| `address` | varchar(1024) | 地址 · 可空 |
| `gender` | varchar(8) | 性别 |
| `nationality` | varchar(255) | 国籍 |
| `mobile` | varchar(64) | 手机号 |
| `id_num` | varchar(255) | 身份证编号 |
| `id_exp` | date | id过期时间 |
| `birth_day` | date | 生日 |
| `id_type` | varchar(32) | id类型 |
| `status` | varchar(4) | 虚拟卡状态：I-inactive，A-active,C-Close,E-Expiry,CB-Conblock银行端拒绝 |
| `payby_status` | varchar(4) | payby状态：A-Active,B-Block用户设置 · 可空 |
| `customer_status` | varchar(4) | 用户状态：A-Active,SU-Suspend风控拒绝 · 可空 |
| `report_time` | timestamp | 上报时间 · 可空 |
| `cancel_time` | timestamp | 注销时间 · 可空 |
| `is_wps` | varchar(4) | 是否是默认wps |
| `back_photo` | varchar(64) | 反面照片 · 可空 |
| `front_photo` | varchar(64) | 正面照片 · 可空 |
| `photo_report_status` | varchar(4) | 照片上报状态 · 可空 |
| `photo_report_time` | timestamp | 照片上报状态 · 可空 |
| `document_tag` | varchar(128) | document文件标识 · 可空 |
| `passport_photo_tag` | varchar(64) | 护照首页照片 · 可空 |
| `status_fetch_tag` | varchar(2) | statusFetchTag:Y-可以Fetch; N-不可以 Fetch;啥都没有同Y · 可空 |
| `allocate_type` | varchar(8) | 开卡类型：COMA-COMMON ALLOACATE; VIPA-VIP CLOSE ALLOCATE · 可空 |
| `extension` | varchar(128) | 扩展参数 · 可空 |
| `upload_count` | int | 上传次数 |

## 主键 / 索引
- 主键:`id`
- `uk_memberId_idType`:member_id, id_type (UNIQUE)
- `idx_cardNo`:card_no
- `idx_gmt_create`:gmt_create
- `idx_gmt_modify`:gmt_modify, photo_report_status
- `idx_idNum`:id_num
- `idx_report_time`:report_time

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
