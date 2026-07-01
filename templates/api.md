---
# API 对象规范。
id: api_<service>_<name>           # api_ 前缀 + 服务 + 接口名
object_type: API
name: <人类可读接口名>(<英文短名>)
aliases: []
domain: <所属服务的业务域>
status: active
owner: <知识负责人=所属服务域负责人>
reviewer: <评审人>
last_reviewed_at: 'YYYY-MM-DD'
source_type: <接口文档|wiki|uat_kibana|...>
source_ref: <来源>
tags: []
related_services: [svc_<owning_service>]   # ★ 反指所属服务(服务正文用 [[api_…]] 反查本接口)
related_tables: [tbl_x]                     # 读写的表(可选)
related_scenarios: [scn_x]                  # 覆盖的测试场景(可选)
---

# <接口名>

## 用途
这个接口做什么、在什么业务场景/流程里被调用。一句话定位 + 必要展开。

## 关联关系
- **所属服务**:[[svc_<owning>]](= frontmatter `related_services`)
- **读写的表**:[[tbl_x]] …(= `related_tables`;不清楚标「待补」)
- **被哪些场景测**:[[scn_x]] …(= `related_scenarios`)
- **自动化 / 流程**:经由场景间接关联([[auto_x]] 覆盖 [[scn_x]] → 测本接口;或出现在 [[flow_x]] 中)。

## 路径 / 方法
- 路径:`/path/to/api`
- 方法:POST / GET

## 入参
| 参数 | 类型 | 必填 | 示例 | 说明 |
| --- | --- | --- | --- | --- |
| ... | ... | Y/N | ... | ...(敏感字段注明加密,如 RSA/密文) |

## 出参
| 参数 | 类型 | 必填 | 示例 | 说明 |
| --- | --- | --- | --- | --- |
| ... | ... | Y/N | ... | ...(嵌套对象用 `--字段` 缩进表示层级) |

## 错误码
| code | 含义 | 触发条件 |
| --- | --- | --- |
| ... | ... | ...（**原文若缺,写「待补:原文未提供错误码」**,便于检索发现、人工补充） |

## 测试校验点(QA)
- 正常/异常分支、边界、幂等、DB 落库点、与上下游接口的联动校验。
- **缺失的点也写在这里(标「待补」),将来检索可发现,人工更新。**
