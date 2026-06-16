- 在agent开发如果一个mcp的内容有需要多个mcp合作链路完成需要对mcp内容进行细化和拆分比如 MRP内容需要去 wms 去采购 去mes 就要做对应的mcp 如wms mcp mesmcp等
- skill过多怎么正常加载  
    1 优化名字 和描述 以及对于何时用具体说明  
    2分类 大类 小类 禁止将skills平铺  
    3什么时候不要用 如仅用于  
    4 不要让大模型平铺选而是 embeding做召回top10  
    skills的加载不是一次性而是通过名字加载
- 业务形态上像多 Agent 协调”，但“工程落地上可以先从单 Agent + 多 MCP 开始  
    到后期进行agent mcp专业化
- 