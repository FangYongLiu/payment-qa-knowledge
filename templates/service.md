---
# ───────── Frontmatter:身份 / 交叉引用 / 治理 ─────────
id: svc_<name>                      # 唯一 id,svc_ 前缀;同一真实服务只用一个 id
object_type: Service
name: <服务名>                       # 人类可读名(代码/部署名进 aliases,别当 name)
aliases: [gpXXX_<name>, <别名>]      # trace 名/前缀名/俗称都列上,便于按别名检索到本对象
domain: <业务域>                     # 业务归属;必须 == 一级目录名(见 index/domains.yaml)
app_group: gpXXX                    # 所属可部署 APP(同 APP 多模块共享)
layer: <架构层,可选>                 # Gateway/Biz Service/Payment Middle Office/... 对齐架构图
status: active                      # active=已审;draft=待管理员审批
owner: <知识负责人>                  # ★ 知识 owner/reviewer:以业务域映射为准(≠dev_owner)
reviewer: <评审人>
dev_owner: <开发联系人>              # 开发侧,排障/提需求找谁(参考,非知识负责人)
last_reviewed_at: 'YYYY-MM-DD'
source_type: <app_inventory|uat_kibana|...>   # 溯源:这条知识哪来的
source_ref: <来源标识>
tags: []
# ───────── 以下 related_* 是指向其它对象的交叉引用(读者据此跳转)─────────
related_services: [svc_a, svc_b]    # ★ 调用的下游服务
related_tables: [tbl_x, tbl_y]      # 读写的库表
related_scenarios: [scn_z]          # 覆盖的测试场景
# 注:服务↔API 的引用由 **API 对象的 related_services**(api→svc)声明,服务侧不重复列;
#     本服务的 API 在正文「涉及的 API」用 [[api_…]] 链接列出即可。
---

# <服务名>

> 来源/置信一行:从哪观测/推断、是否待核实。

## 作用
一句话定位 + 展开:这个服务在系统里负责什么。推断的标 **(待核实)**。

## 系统中的位置
- 功能层:<架构层>
- 业务域:`<domain>`(owner / dev_owner)
- 参与的业务流:[[flow_xxx]]

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_a]] a(作用短标) · <频次> · high/med
**被调用(上游)—— 谁调本服务:**
- <上游服务列表>

## 涉及的 API / 数据库表
- **暴露/相关 API**:[[api_p]] …(QA 接口测试入口)
- **读写的表**:[[tbl_x]] …(QA 落库检查点)

## 关键方法 / 入口
- 观测到的对外方法:<method>;入口 API path:<path>

## 测试要点 / 排障 / 常见问题
- ★ QA 视角最高价值:怎么测、已知坑、注意点、典型故障与定位。(从 scenario/排障经验/团队补)

## 来源与置信
- 数据窗口 / 推断标记 / 待核实项。
