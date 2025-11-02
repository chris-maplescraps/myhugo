+++
title = 'Langchain Code'
date = 2025-11-01T20:51:57+08:00
draft = false
slug = "bbe7cd1"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# Langchain Code
## 硬编码方式
#### 演示对话模型
> ```python
> # 导入langchain模块
> from langchain_openai import ChatOpenAI
> 
> # 配置对话模型
> chat_model = ChatOpenAI(
> 		# 必须要设置的3个参数
> 		model_name="gpt-4o-mini", # 默认使用的是gpt-3.5-turbo模型
> 		base_url="https://api.openai-proxy.org/v1",
> 		api_key="xxxxxxxxxxxxxxxxxxxxxxxxxxxx"
> )
> 
> # 调用模型
> response = chat_model.invoke("什么是langchain?")
> 
> # 查看响应文本
> print(response.content)
> ```

---

#### 演示非对话模型
> ```python
> # 导入langchain模块
> from langchain_openai import OpenAI
> 
> # 配置对话模型
> llm = OpenAI(
> 		# 必须要设置的3个参数
> 		# model_name="gpt-4o-mini", # 默认使用的是gpt-3.5-turbo模型
> 		base_url="https://api.openai-proxy.org/v1",
> 		api_key="xxxxxxxxxxxxxxxxxxxxxxxxxxxx"
> )
> 
> # 调用模型
> response = llm.invoke("什么是langchain?")
> 
> # 查看响应文本
> print(response)
> ```
> 

---

## 环境变量方式
#### 使用 `.env` 的配置文件
##### 创建 `.env` 文件
> ```.env
> OPENAI_API_KEY1="xxxxxxxxxxxxxxxxxxxx"
> OPENAI_BASE_URL="xxxxxxxxxxxxxxxxxxxx"
> 
> # 阿里云百炼平台
> DASHSCOPE_APY_KEY="xxxxxxxxxxxxxxxxxx"
> DASHSCOPE_BASE_URL="xxxxxxxxxxxxxxxxxx"
> 
> # 智谱
> ZHIPUAI_API_KEY="xxxxxxxxxxxxxxxxxxxx"
> ZHIPUAI_URL="xxxxxxxxxxxxxxxxxxxxxxx"
> 
> # 硅基流动
> SILICON_API_KEY="xxxxxxxxxxxxxxxxxxxx"
> ```

> ##### 示例一
> ```python
> # 导入langchain模块
> from langchain_openai import ChatOpenAI
> import dotenv
> import os
> 
> # 读取.env文件（💡 默认情况下，load_dotenv() 会自动在项目根目录查找 .env 文件）
> dotenv.load_dotenv()
> 
> # 配置对话模型
> chat_model = ChatOpenAI(
> 		# 必须要设置的3个参数
> 		model_name="gpt-4o-mini", # 默认使用的是gpt-3.5-turbo模型
> 		base_url=os.getenv("OPENAI_BASE_URL"),
> 		api_key=os.getenv("OPENAI_API_KEY"),
> )
> 
> # 调用模型
> response = chat_model.invoke("什么是langchain?")
> 
> # 查看响应文本
> print(response)
> ```
> 

> ##### 示例二
> ```python
> # 导入langchain模块
> from langchain_openai import ChatOpenAI
> import dotenv
> import os
> 
> # 读取.env文件（💡 默认情况下，load_dotenv() 会自动在项目根目录查找 .env 文件）
> dotenv.load_dotenv()
> 
> # 设置环境变量值
> os.environ["OPENAI_BASE_URL"] = os.getenv("OPENAI_BASE_URL")
> os.environ["OPENAI_API_KEY"] = os.getenv("OPENAI_API_KEY1")
> 
> # 配置对话模型
> chat_model = ChatOpenAI(
> 		# 必须要设置的3个参数
> 		model_name="gpt-4o-mini", # 默认使用的是gpt-3.5-turbo模型
> 		# base_url=os.getenv("OPENAI_BASE_URL"),
> 		# api_key=os.getenv("OPENAI_API_KEY"),
> )
> 
> # 调用模型
> response = chat_model.invoke("什么是langchain?")
> 
> # 查看响应文本
> print(response)
> ```
> 补充：  
> 当 `ChatOpenAI( )` 当没有声明 `base_url` 和 `api_key` 的时候，默认会从环境变量中查找  
> 可以参考 `ChatOpenAI( )` 文档   
> 

---

#### 其他参数说明
> `temperature`：控制生成文本的 ' 随机性 '，取值范围 0 ~ 1  
>> - 值越低 --> 输出越确定，保守（适合事实回答）  
>> - 值越高 --> 输出越多样，有创意（适合创意写作）  
>> ##### 需求设置参考：  
>> - 精准模式（ 0.5 或更低 ）--> 生成的文本更加安全可靠，但可能缺乏创意和多样性  
>> - 平衡模式（ 一般是 0.8 ） --> 生成的文本通常既有一定的多样性，又能保持较好的连贯性和准确性  
>> - 创意模式（ 一般是 1 ） --> 生成的文本更有创意，但也更容易出现语法错误或不合逻辑的内容  

> `max_tokens`：限制生成文本的最大长度，防止输出过长
>> Token 是什么？
>> 