# 知识文档编写规范(上传 / 新建文档前必读)

> 目标:**有血肉 + 全连边**。每个文档按模板写够内容(血肉),并且**每新增一个对象,
> 都回头更新所有相关对象的关联信息**(连边)。只有这样,reindex 出来的知识图谱才是系统的真实镜像。

---

## 0. 两条铁律
1. **按模板写**:每类对象用 `templates/<类型>.md` 的 frontmatter + 正文小节,一节不少。
2. **新增即回写**:新建任何一个 `.md`,必须按 §4 的清单更新**其它已存在文档**的关联信息——
   不是只写自己,而是把自己织进网里。漏回写 = 有叶子无主干。

不确定 / 查不到的内容:统一标 **「待补」**,不要臆造。标了待补,检索时能发现,人工再补充更新。

---

## 1. 八类对象 + 命名
| 类型 | id 前缀 | 文件名 | 何时用 |
| --- | --- | --- | --- |
| Service | `svc_` | `service_<app_group>_<name>.md` | 一个可部署服务/应用 |
| API | `api_` | `api_<service>_<name>.md` | 一个接口 |
| Table | `tbl_` | `tbl_<schema>_<table>.md` | 一张库表 |
| Scenario | `scn_` | `scn_<域>_<name>.md` | 一个业务测试场景 |
| Flow | `flow_` | `flow_<name>.md` | 一条端到端流程 |
| Troubleshooting | `ts_` | `ts_<symptom>.md` | 一个排障/故障案例 |
| AutomationAsset | `auto_` | `auto_<域>_<name>.md` | 一套自动化资产(测试套件) |
| Domain | `domain_` | `domain_<slug>.md` | 一个业务域总览 |

**文件名带 `app_group`**(服务),其它对象文件名带所属域/服务,风格统一。

---

## 2. Frontmatter(机器读:身份 + 图边 + 治理)
- `id` 唯一、前缀正确;**改文件名不改 id**(reindex 按 id 重建,改名对图谱透明)。
- `owner` / `reviewer`:**知识负责人,按 12 业务域映射**(见 `index/domains.yaml`),≠ `dev_owner`(开发联系人)。
- `status: active` 才进生产检索;`domain` 必填(未认领填 `service-catalog`)。
- `app_group` / `layer`:Service 专有;其它类型不用。
- **`related_*` 就是图的边**(见 §3)。

---

## 3. 关系模型(连边的机制,务必理解)
**只有这 6 个 frontmatter 字段会生成图边**:

| 字段 | 边 | 指向 |
| --- | --- | --- |
| `related_services` | uses_service | 服务 |
| `related_tables` | reads_table | 表 |
| `related_scenarios` | covered_by_scenario | 场景 |
| `related_failures` | has_failure | 故障 |
| `related_logs` | logged_in | 日志(伪节点) |
| `related_requirements` | impacts_requirement | 需求(伪节点) |

要点:
- **正文里的 `[[链接]]`,在 typed 对象中不生成边**(只有 wiki 页的 `[[]]` 生成 `references` 边)。
  正文 `[[]]` 是给人看/导航;真正的边在 frontmatter `related_*`。
- **单边声明**:每条边只从"自然源头"声明一次,不双向重复(否则重复边 + 维护漂移)。
  `impact_analysis` 走**双向遍历**,单边声明两头都能查到。
- **没有 `related_apis` 字段**:服务↔API 的边由 **API 的 `related_services`** 提供(api→svc)。
- **不要指向不存在的对象**(会产生悬空边)。对象还没建时,在正文写名字 + 标「待补」,别硬连。

### 边归属矩阵(谁声明什么)
| 对象 | 自己声明的 related_* |
| --- | --- |
| Service | services(下游)/ tables / scenarios |
| API | services(所属)/ tables / scenarios |
| Table | services(所属)/ scenarios |
| Scenario | services / tables / logs |
| Flow | services / tables / scenarios |
| Troubleshooting | services / tables / logs / failures |
| Domain | services(关键服务) |
| AutomationAsset | scenarios / services |

---

## 4. ★ 新增对象时的回写清单(全连边的核心)
新建一个对象后,**按下表回头更新相关文档**(frontmatter 边 + 正文 `[[链接]]` 都要):

- **新增 Service**
  - `domain_<域>.md` 的「关联关系」加 `[[svc_x]]`(并把它写进 `related_services`)
  - 它的上下游服务:由**调用方**在 `related_services` 声明
- **新增 API**
  - 所属 `service_*.md` 正文「涉及的 API / 数据库表」加 `[[api_x]]`
  - `api_x.related_services = [svc]`;已知则补 `related_tables` / `related_scenarios`
- **新增 Table**
  - 所属 `service_*.md` 正文「涉及的…表」加 `[[tbl_x]]`
  - 读写它的 Service / API:在各自 `related_tables` 加 `tbl_x`
- **新增 Scenario**
  - `scn_x.related_services` / `related_tables`
  - 被它测的每个 `api_*.md`:`related_scenarios` 加 `scn_x` + 正文「被哪些场景测」加 `[[scn_x]]`
  - 覆盖它的 `auto_*.md`:`related_scenarios` 加 `scn_x`
- **新增 AutomationAsset**
  - `auto_x.related_scenarios`(覆盖的场景)/ `related_services`(跑在/针对的服务)
  - 它调用的每个 `api_*.md`:正文「被哪些自动化覆盖」加 `[[auto_x]]`
  - 它覆盖的每个 `scn_*.md`:正文「覆盖它的自动化」加 `[[auto_x]]`
  - 所属 `service_*.md` / `domain_*.md` 正文加 `[[auto_x]]`
- **新增 Domain**
  - `related_services` = 该域关键服务;「关联关系」列关键服务 / 流程 / 自动化

> 经验法则:**任何 A→B 的关系,A 和 B 两个文档都要能看到对方**(一边靠 frontmatter 边,另一边靠正文链接 + 反向边)。

---

## 5. 完整样板:kyc 域
kyc 是第一个"有血肉 + 全连边"的样板域,结构可照搬:

```
domain_kyc (1)
  └─ service_gp078_kyc / service_gp202_kyc_service (2)
       ├─ api_kyc_* (33)
       ├─ scn_kyc_* (5)        ← 从 cgs-apitest 自动化用例整理
       └─ auto_kyc_* (2)       ← cgs-apitest 测试套件
```
连边:domain→service(`related_services`)、api→service、scn→service、auto→scn、api↔scn;
正文交叉链接:service 列 API/自动化、api 标"被哪些场景/自动化测"、scn 列走过的接口、auto 列覆盖场景+调用接口。

**整理过程(可复用的步骤)**:
1. 读源(如 `cgs-apitest/testcases/.../test_*.py`),理解每个用例做什么。
2. 按业务场景归并成 Scenario(排除纯测试夹具),写 `scn_*.md`。
3. 把测试套件写成 `auto_*.md`,`related_scenarios` 指向上一步的场景。
4. **回写**:被覆盖的 `api_*` 补 `related_scenarios` + 正文;service / domain 正文补「自动化资产」。
5. 不确定的(表结构、失败分支)标「待补」。

---

## 6. 提交前自检
- 每个新文档:frontmatter 字段齐全、正文小节齐全(对照 `templates/<类型>.md`)。
- `related_*` 不指向不存在的对象(无悬空边)。
- 回写清单(§4)都做了——新对象在相关文档里都能被看到。
- 不确定的都标了「待补」,没有臆造。
