+++
title = 'Hugo_syntax'
date = 2025-10-02T08:21:28+08:00
draft = false
slug = "560e275"
description = ""
summary = ""
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# Hugo_syntax

> [!NOTE]+ hugo 语法库:
> #### Shortcode 语法结构
> - **{{</* ... */>}} (尖括号)**: 用于 Shortcode 结果不会被 Markdown 处理器再次处理的情况，通常用于插入复杂的 HTML 结构，比> 如> 图片 (figure) 或卡片。 
> - **{{%/* ... */%}} (百分号)**: 用于 Shortcode 结果需要被 Markdown 处理器再次处理的情况。由于 > {{%/* param "" */%}} 的结果通常是文本（如 "red"），Markdown 处理器需要能够将这段文本作为普通内容的一部分来渲染，因此必> 须使用百分号版本。

> #### 常用 Shortcode 示例
> - **{{</* figure ... */>}}**: 插入图片或视频，支持 caption、link 等参数。
>> 示例 : 
>>
>>{{</* figure **src="/images/xxx.jpg"** **alt="xxx"** **caption="xxx"** **link="https://xxx"** **class="w-75 ma0"** */>}}

> - **{{</* link ... */>}}**: 插入可点击的链接，支持 target="_blank" 等参数。
> - **{{</* param ... */>}}**: 插入参数值，用于动态内容。

> [!NOTE]+ Instagram shortcode
> #### Example
> To display an Instagram post with this URL:
>> `https://www.instagram.com/p/CxOWiQNP2MO/`
>
> Include this in your Markdown:
>> ` {{</* instagram CxOWiQNP2MO */>}}`

> [!NOTE]+ HightLight shortcode
> #### Example
>> {{< highlight go "linenos=inline, hl_lines=1-10, style=emacs" >}}
package main

import "fmt"

func main() {
    for i := 0; i < 3; i++ {
        fmt.Println("Value of i:", i)
    }
}
>>{{< /highlight >}}
>>
> #### You can also use the highlight shortcode for inline code snippets:
>> This is some {{< highlight go "hl_inline=true" >}}fmt.Println("inline"){{< /highlight >}} code.
>>
>>  **{{</* highlight go "hl_inline=true" */>}}** Your_text_highlight **{{</* /highlight */>}}**