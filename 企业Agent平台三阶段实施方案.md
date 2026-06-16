# 企业Agent平台三阶段实施方案

## 一、项目目标

构建面向制造业企业的智能Agent平台，实现ERP、WMS、MES、PLM等系统的统一接入，通过自然语言驱动业务流程执行，逐步从规则驱动演进到智能决策。

总体架构：

```text
用户
 ↓
Agent
 ↓
Workflow
 ↓
Tool
 ↓
MCP
 ↓
ERP/WMS/MES/PLM/SRM
```

---

# 第一阶段：MCP + Workflow基础平台

## 阶段目标

建立企业Agent运行基础设施。

实现：

- MCP统一接入
    
- Tool注册中心
    
- Workflow编排引擎
    
- LLM意图识别
    

此阶段不考虑多Agent。

---

## 架构

```text
用户
 ↓
LLM
(意图识别)

 ↓

Workflow Engine

 ↓

Tool Registry

 ↓

Tool

 ↓

MCP

 ↓

ERP/WMS/MES/PLM
```

---

## 核心模块

### 1.MCP层

统一封装企业系统。

#### ERP MCP

```text
采购申请
采购订单
供应商
销售订单
```

#### WMS MCP

```text
库存
库位
出库
入库
```

#### MES MCP

```text
工单
报工
产能
设备
```

#### PLM MCP

```text
BOM
产品资料
工艺路线
```

---

### 2.Tool Registry

维护Tool与MCP映射关系。

示例：

```json
{
  "query_bom":"plm_mcp",
  "query_inventory":"wms_mcp",
  "query_po":"erp_mcp"
}
```

---

### 3.Workflow Engine

负责执行编排。

示例：

```yaml
workflow:
  material_shortage_analysis

steps:
  - query_bom
  - query_inventory
  - query_po
  - calculate_gap
```

---

### 4.Context

用于保存流程数据。

```java
public class WorkflowContext {

    String productCode;

    Integer quantity;

    List<String> materials;

    Map<String,Integer> inventory;

    Map<String,Integer> inTransit;

}
```

---

## 第一阶段可落地场景

### 缺料分析

```text
P100生产500台缺什么料
```

执行：

```text
query_bom
 ↓
query_inventory
 ↓
query_po
 ↓
calculate_gap
```

---

### 库存查询

```text
A001库存是多少
```

执行：

```text
query_inventory
```

---

### 工单查询

```text
WO202501状态
```

执行：

```text
query_work_order
```

---

## 阶段成果

实现：

```text
Agent平台V1
```

具备：

```text
自然语言
+
流程编排
+
企业系统接入
```

能力。

---

# 第二阶段：智能Agent平台

## 阶段目标

让Agent具备自主规划能力。

从：

```text
固定Workflow
```

升级到：

```text
动态Workflow
```

---

## 架构升级

```text
用户

 ↓

Agent Planner

 ↓

Workflow Generator

 ↓

Tool

 ↓

MCP
```

---

## 新增模块

### Planner Agent

负责分析用户意图。

例如：

```text
P100生产500台
帮我看看缺料
并生成采购申请
```

Planner生成：

```text
query_bom
 ↓
query_inventory
 ↓
query_po
 ↓
calculate_gap
 ↓
create_purchase_request
```

---

### Dynamic Workflow

运行时动态生成。

无需提前配置。

示例：

```json
{
  "steps":[
    "query_bom",
    "query_inventory",
    "query_po",
    "calculate_gap",
    "create_pr"
  ]
}
```

---

### Knowledge Base

接入：

```text
ERP文档
制度文件
SOP
BOM规范
操作手册
```

形成企业知识库。

---

### RAG能力

实现：

```text
文档问答
制度查询
知识搜索
```

---

## 第二阶段场景

### 智能采购助手

```text
根据缺料情况生成采购建议
```

---

### 智能生产助手

```text
分析工单延期原因
```

---

### 智能库存助手

```text
分析库存积压原因
```

---

## 阶段成果

实现：

```text
Agent平台V2
```

具备：

```text
自主规划
+
知识库
+
动态Workflow
```

能力。

---

# 第三阶段：多Agent协同平台

## 阶段目标

构建企业数字员工体系。

---

## 架构

```text
用户

 ↓

总控Agent

 ├──采购Agent
 ├──生产Agent
 ├──仓储Agent
 ├──销售Agent
 └──财务Agent

 ↓

Workflow

 ↓

Tool

 ↓

MCP
```

---

## Agent划分

### 采购Agent

负责：

```text
采购申请
供应商分析
采购订单跟踪
```

---

### 仓储Agent

负责：

```text
库存分析
出入库分析
库龄分析
```

---

### 生产Agent

负责：

```text
工单分析
排产分析
产能分析
```

---

### 财务Agent

负责：

```text
费用分析
利润分析
成本核算
```

---

## Agent协同案例

用户：

```text
P100生产500台
请评估是否可以按时交付
```

总控Agent：

```text
拆解任务
```

---

生产Agent：

```text
分析产能
```

---

仓储Agent：

```text
分析库存
```

---

采购Agent：

```text
分析缺料
```

---

财务Agent：

```text
分析采购成本
```

---

最终汇总：

```text
交付风险报告
```

---

## 高级能力

### 人工审批节点

```text
Agent
 ↓
生成采购申请
 ↓
审批人确认
 ↓
继续执行
```

---

### 长流程编排

接入：

```text
Camunda
Temporal
Flowable
```

---

### 事件驱动

接入：

```text
RabbitMQ
Kafka
RocketMQ
```

---

### 数据分析

接入：

```text
BI
数据仓库
Data Lake
```

---

## 阶段成果

实现：

```text
Agent平台V3
```

能力：

```text
多Agent协同
+
跨部门协作
+
自动决策
+
数字员工
```

---

# 技术栈建议

## 后端

```text
Java 21
Spring Boot 3.x
Spring Cloud Alibaba
MyBatis Plus
Redis
MySQL
RabbitMQ
```

---

## AI层

```text
OpenAI GPT-5.5
Qwen3
DeepSeek
```

---

## Workflow

V1：

```text
自研Workflow Engine
```

V2：

```text
LangGraph
```

V3：

```text
Temporal
Camunda
```

---

## MCP

```text
ERP MCP
WMS MCP
MES MCP
PLM MCP
SRM MCP
CRM MCP
```

---

# 实施顺序

```text
第一阶段
MCP + Workflow
        ↓

第二阶段
Planner + RAG
        ↓

第三阶段
Multi-Agent
```

优先完成第一阶段，再进入后续演进。
