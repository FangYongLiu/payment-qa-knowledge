---
# ───────── Frontmatter:机器读(身份 / 图边 / 治理)。reindex 解析,related_* 即图的边。─────────
id: svc_<name>                      # 唯一 id,svc_ 前缀;实体消解的主键
object_type: Service
name: <服务名>                       # 人类可读名(代码/部署名进 aliases,别当 name)
aliases: [gpXXX_<name>, <别名>]      # ★ 实体消解:trace 名/前缀名/俗称都列上,建图防重复节点
domain: <12 业务域之一 | service-catalog>   # 业务归属;路由 + 按域分区;未认领=service-catalog
app_group: gpXXX                    # 所属可部署 APP(同 APP 多模块共享)
layer: <架构层,可选>                 # Gateway/Biz Service/Payment Middle Office/... 对齐架构图
status: active                      # active 才进生产检索;draft/archived 不进
owner: <知识负责人>                  # ★ 知识 owner/reviewer:以 12 QA 域映射为准(≠dev_owner)
reviewer: <评审人>
dev_owner: <开发联系人>              # 开发侧,排障/提需求找谁(参考,非知识负责人)
last_reviewed_at: 'YYYY-MM-DD'
source_type: <app_inventory|uat_kibana|...>   # 溯源:这条知识哪来的
source_ref: <来源标识>
tags: []
# ───────── 以下 related_* 是图的边(reindex → knowledge_relations)─────────
related_services: [svc_a, svc_b]    # ★ 调用的下游服务 → uses_service 边(核心)
related_tables: [tbl_x, tbl_y]      # 读写的库表 → reads_table 边
related_apis: [api_p, api_q]        # 暴露/涉及的接口(★ 需 schema 支持;暂可用 api 端 related_services 反向)
related_scenarios: [scn_z]          # 覆盖的测试场景 → covered_by_scenario 边
---

# <服务名>

> 来源/置信一行:从哪观测/推断、是否待核实。

## 作用
一句话定位 + 展开:这个服务在系统里负责什么(③④的总纲,embedding 检索主体)。
推断的标 **(待核实)**。

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
- **暴露/相关 API**:[[api_p]] …(service↔api 边;QA 接口测试入口)
- **读写的表**:[[tbl_x]] …(service↔table 边;QA 落库检查点)

## 关键方法 / 入口
- 观测到的对外方法:<method>;入口 API path:<path>

## 测试要点 / 排障 / 常见问题
- ★ QA 视角最高价值:怎么测、已知坑、注意点、典型故障与定位。(从 scenario/排障经验/团队补)

## 来源与置信
- 数据窗口 / 推断标记 / 待核实项。
