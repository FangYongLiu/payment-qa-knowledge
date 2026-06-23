---
# AutomationAsset 对象规范(与 _SKELETONS[AutomationAsset] 对齐)。
id: auto_<name>
object_type: AutomationAsset
name: <自动化资产名>
aliases: []
domain: <业务域>
status: active
owner: <域 owner(12 域映射)>
reviewer: <评审人>
last_reviewed_at: 'YYYY-MM-DD'
source_type: <repo|manual|...>
source_ref: <来源(仓库/路径)>
tags: []
related_scenarios: []                # 覆盖的测试场景
related_services: []
---

# <自动化资产名>

## 用途
这套自动化做什么、覆盖哪些场景。

## 关联关系
- **覆盖的场景**:[[scn_x]](= `related_scenarios`)
- **针对 / 跑在的服务**:[[svc_x]](= `related_services`)

## 使用方式
- 怎么跑、在哪跑(仓库 / 命令 / 流水线)。

## 关键配置
- 环境 / 数据 / 账号依赖。

## 注意事项
- flaky / 环境 / 数据坑;维护者。
> 不确定 / 缺失标「待补」。
