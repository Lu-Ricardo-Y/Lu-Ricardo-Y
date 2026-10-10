[English](./README.md) · **简体中文**

# Lu-Ricardo-Y

我最近主要在做 AI Agent 和 RAG 相关的项目。相比让模型多说几句话，我更关心它依据什么回答、什么时候该拒答、调用工具前需要哪些约束，以及怎么把失败案例留在评测里。代码主要用 Python 和 Go。

## Merchant Support Agent

这是我目前最想展示的项目：一个面向电商售后场景的知识问答与工单 Agent。我把它做成了从政策检索、回答到工单处理的完整流程，而不只是一个聊天界面。项目使用模拟政策、订单和工单数据，没有接入真实电商平台。

我先整理了带版本、生效状态和章节信息的政策文档，并写了 120 条人工标注用例，覆盖直接问答、例外条件、多文档问题、旧版政策冲突、证据不足、工具调用和人工确认。检索部分同时使用 BM25 和本地 BGE 向量模型：前者擅长政策术语、数字和版本号，后者更能接住口语化问法，再用 RRF 合并两路结果。

回答层接入 Qwen，但证据边界和引用不交给模型自由发挥。系统先检查检索内容是否足以支持问题，再由后端根据实际来源生成引用；遇到政策没有覆盖的限定条件时，会拒绝给出确定承诺。Agent 还可以查询工单。创建工单时，它先给出待确认计划，只有用户明确确认后才写入 SQLite；工具层会再次检查确认状态，并用参数校验和幂等键避免重复写入。

我也保留了不那么好看的结果。首次隔离测试中，混合检索的 Recall@5 是 **94.59%**，但 RAG 行为匹配率只有 **75%**；“建高优先级工单”这样的表达还暴露了意图识别缺口。修复后我把这些案例加入回归测试，没有用重跑后的数字覆盖首次盲测。项目提供 Docker 启动、演示页面、运行追踪，以及检索、回答和 Agent 路由的评测脚本。

[项目代码](https://github.com/Lu-Ricardo-Y/merchant-support-agent) · [评测结果与失败分析](https://github.com/Lu-Ricardo-Y/merchant-support-agent/blob/main/docs/RESULTS.md) · [演示截图](https://github.com/Lu-Ricardo-Y/merchant-support-agent/tree/main/docs/images)

## 其他项目

**[AgentGate](https://github.com/Lu-Ricardo-Y/AgentGate)** 是一个 Go 写的 Agent 安全执行参考实现，使用本地 Ollama 模型，重点处理租户与资源权限、写操作审批、审计记录和失败状态。它是与 [@kimzclandi](https://github.com/kimzclandi) 合作的项目，具体贡献见 [AUTHORS.md](https://github.com/Lu-Ricardo-Y/AgentGate/blob/main/AUTHORS.md)。

**[Bearing Fault Diagnosis](https://github.com/Lu-Ricardo-Y/bearing-fault-diagnosis)** 是合作维护的 fork，基于 CWRU 振动数据做信号处理、轴承故障分类、物理频率特征和鲁棒性测试，也有 Streamlit 演示。项目把健康指数限定为记录内的偏离变化，没有把它说成剩余寿命预测。
