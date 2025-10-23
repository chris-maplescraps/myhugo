+++
title = 'Streamlit'
date = 2025-10-23T14:44:37+08:00
draft = false
slug = "9297db3"
description = ""
summary = ""
tags = [ "技术", "AI", "Python" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"

+++

# Streamlit

#### Streamlit 是一个开源的 Python 框架（ 库 ） [ offical link ]( https://docs.streamlit.io/ )

##### 它最主要的目的是让**数据科学家**和**机器学习工程师**能够**快速、简单地创建和分享交互式的 Web 应用**，而**无需具备任何前端（ HTML、CSS、JavaScript ）的 Web 开发技能**。    

> #####  :notebook_with_decorative_cover: 需要安装 2 个库   
> - uv add streamlit 
> - uv add ollama

##### :sweat_drops::sweat_drops::sweat_drops: 以下示例是实现利用 Streamlit 和 Ollama AI模型创建交互式的 Web 应用

```python
import streamlit as st
import ollama

client = ollama.Client(host="http://localhost:11434")

# 定义 message 空列表，用于保存聊天记录
# 如果 st.session_state 没有 message 记录，则创建新的空列表
if "message" not in st.session_state:
    st.session_state["message"] = []

# 设置标题
st.title("智聊机器人")

# 添加分割线
st.divider()

# 设置内容输入框
prompt = st.chat_input("请输入您的内容")

# 判断，如果 prompt 有内容，则开始执行条件
if prompt:
    # 将用户提问信息添加到历史记录
    st.session_state['message'].append({"role": "user", "content": prompt})
    # 遍历所有历史信息，然后输出到消息容器内
    for message in st.session_state['message']:
        st.chat_message(message['role']).markdown(message['content'])
	# 实现 AI 思考动画
    with st.spinner("AI思考中..."):
    	# 调用 deepseek-r1:last 模型进行回答
        response = client.chat(
            model="deepseek-r1:latest",
            messages=[{"role": "user", "content": prompt}]
        )

        # 从 response 去除 message 和 content 两个 key
        st.session_state['message'].append({"role": "assistant", "content": response['message']['content']})

        # 在页面中渲染 AI 的内容
        st.chat_message('assistant').markdown(response['message']['content'])

```