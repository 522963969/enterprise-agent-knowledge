- 在agent开发如果一个mcp的内容有需要多个mcp合作链路完成需要对mcp内容进行细化和拆分比如 MRP内容需要去 wms 去采购 去mes 就要做对应的mcp 如wms mcp mesmcp等
- skill过多怎么正常加载  
    1 优化名字 和描述 以及对于何时用具体说明  
    2分类 大类 小类 禁止将skills平铺  
    3什么时候不要用 如仅用于  
    4 不要让大模型平铺选而是 embeding做召回top10  
    skills的加载不是一次性而是通过名字加载
- 业务形态上像多 Agent 协调”，但“工程落地上可以先从单 Agent + 多 MCP 开始  
    到后期进行agent mcp专业化
- 如果mcp 多了agent 消耗token 和选择工具错误率高
    Tool Registry工具注册中心可以用来减少误判和tool的管理
    Agent 调 Tool Registry给出 候选 Tool最后的选择是LLM
    Tool Registry 解决“用什么工具”  
    Workflow 解决“怎么用这些工具”![[Pasted image 20260617143946.png]]
- mcp编写流程
    把能力拆成 Tool 并暴露给 AI 调用
    【1】Tool 定义层（能力声明层） 描述能力
    【2】Tool 执行层（业务实现层）执行逻辑
    【3】MCP 协议层（对外通信层）controller +gateway AI通信
   开发流程
   【1】Tool 定义（能力描述）  
	【2】Tool 注册（进入Registry）  
	【3】Tool 执行（业务实现）  
	【4】MCP 协议暴露（tools/list + tools/call）
	Codex不需要外置ToolRegistry，  是因为：  
	 MCP Server本身已经实现了“最小可用Tool Registry能力（tools/list）”  
    但企业级系统必须外置Registry来做治理、检索和跨MCP调度。
    
