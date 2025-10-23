+++
title = 'Langchain AI'
date = 2025-10-23T15:41:01+08:00
draft = false
slug = "de862c4"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Langchain AI

##### LangChain 是用于构建基于**大型语言模型（LLM）\**应用程序的\**开源框架（Framework）**。  

##### LangChain 框架由几个核心模块组成，以实现上述功能：

1. **Models (模型)**: 封装了与不同 LLM 提供商（如 OpenAI, HugingFace）的连接接口。
2. **Prompts (提示词)**: 提供了管理、构建和优化发送给 LLM 的提示词的工具。
3. **Chains (链)**: 将多个 LLM 调用和/或其他组件连接在一起形成端到端的应用。
4. **Retrieval (检索)**: 用于从外部数据源（如向量数据库）获取相关文档，这是 RAG 的核心。
5. **Agents (代理)**: LLM 通过代理做出决策，选择要使用的工具和执行的步骤

##### 💦💦💦 以下示例是实现利用 langchain 和 云平台 AI 模型创建的生成式 AI

```py
from langchain.chains import ConversationChain
from langchain.memory import ConversationBufferMemory
from langchain_community.llms import Tongyi

# 创建一个内存记忆对象
memory = ConversationBufferMemory(return_message=True)

def get_respomse(prompt: str, api_key: str):
    model = Tongyi(model="qwen-max", api_key=api_key)
    chain = ConversationChain(llm=model, memory=memory)
    
    # 发送用户的请求
    response = chain.invoke({"input": prompt})
    return response["response"]

if __name__ == '__main__':
    print(get_response("请用Python输出1-10", api_key))
    
```



