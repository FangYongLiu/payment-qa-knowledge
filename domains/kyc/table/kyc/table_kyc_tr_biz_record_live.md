---
id: tbl_kyc_tr_biz_record_live
object_type: Table
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: DB DDL
source_ref: DataGrip DDL export (kyc schema) 2026-06-24
tags:
- kyc
- eid
- tr_biz_record_live
subdomain: eid
module: null
sensitivity: restricted
name: 活体业务记录表(tr_biz_record_live)
aliases:
- tr_biz_record_live
related_services:
- svc_kyc
related_scenarios:
- scn_kyc_eid_full_journey
---

# 活体业务记录表(tr_biz_record_live)

## 用途
EID **活体核身结果**:活体视频/大礼包图片解析 + 比对分数(`live_face_score`)。`record_id`/`req_token` 关联主流程。对应 liveness/retake-selfie 类接口。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:[[scn_kyc_eid_full_journey]](= `related_scenarios`)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `req_token` | varchar(32) |  | kyc流程token |
| `record_id` | bigint |  | 业务记录ID |
| `req_idn` | varchar(32) |  | 身份证号 |
| `req_video` | varchar(32) |  | 视频 |
| `req_audio_code` | varchar(32) |  | 动态口令 |
| `req_image_package_tag` | varchar(128) |  | 用户提交的大礼包图片 |
| `req_check_image_name` | varchar(128) |  | 依图文件名 |
| `live_unified_no` | varchar(32) |  | 证件唯一编号 |
| `live_idn` | varchar(32) |  | 身份证号 |
| `live_name_arabic` | varchar(32) |  | 阿拉伯名称 |
| `live_name_english` | varchar(32) |  | 英文名称 |
| `live_nationality_ica` | varchar(32) |  | 通道返回国籍 |
| `live_nationality_desc` | varchar(32) |  | 通道返回国籍描述 |
| `live_birth_date` | datetime |  | 出生日期 |
| `live_marital_status` | varchar(32) |  | 婚姻状态 |
| `live_religion` | varchar(32) |  | 信仰 |
| `live_home_land` | varchar(32) |  | 户籍 |
| `live_gender` | varchar(32) |  | 性别 |
| `live_channel_code` | varchar(32) |  | 通道编号 |
| `live_upload_file_name` | varchar(32) |  | 活体认证照片 |
| `live_upload_file_list` | varchar(255) |  | 活体大礼包图片集合 |
| `live_face_score` | varchar(32) |  | 活体对比结果 |
| `resp_next_step` | varchar(32) |  | 下步标识 |
| `resp_code` | varchar(32) |  | 响应编码 |
| `resp_msg` | varchar(255) |  | 响应详细 |
| `exp1` | varchar(150) |  | Extense field |
| `exp2` | varchar(32) |  | 扩展字段2 |
| `create_time` | timestamp |  | 创建日期 |
| `update_time` | timestamp |  | 更新日期 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_live_face`:(`live_upload_file_name`)
- 索引 `idx_rid`:(`record_id`)

## 校验点(QA 关注)
- `live_face_score` 达到阈值才算活体通过;不达标应触发重拍(retake)。
- 活体照片/文件以 tag 引用,不落原图;敏感字段密文。
- resp_next_step 与主流程 step 推进一致。
