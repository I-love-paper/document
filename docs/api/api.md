# 免费的API
**在GitHub上有一个公益项目 [GPT-API-free](https://github.com/chatanywhere/GPT_API_free)**
**感谢项目作者** **chatanywhere** **为我们提供免费的API服务**

![free](https://cdn.jsdelivr.net/gh/I-love-paper/image/image/free.jpg)



# 付费的API

**除了免费API** **GPT-API-free** **还提供了付费的API服务**

![pay](https://cdn.jsdelivr.net/gh/I-love-paper/image/image/pay.jpg)

# API的限制

| 限制| 免费的API | 付费的API |
| -------- | :--- | ---- |
| 国内可用 | ✔ | ✔ |
| 国外可用 | ✔ | ✔ |
| 使用限制 | **60请求/小时/IP** | 无限制 |

**免费API Key限制** **60请求/小时/IP&Key** **调用频率，也就是说**

**如果在一个IP下使用多个Key，所有Key的每小时请求数总和不能超过60，同理，你如果将一个Key用于多个IP，这个Key的每小时请求数也不能超过60。**

# 使用

| **AutoGPT**                         |
| ----------------------------------- |
| **langchain**                       |
| **ChatBox**                         |
| **浏览器插件ChatGPT Sidebar**       |
| **Jetbrains插件ChatGPT - Easycode** |
| **VSCode插件Code GPT**              |
| **Raycast 插件 ChatGPT**            |

# api代码示例



```python
import openai

# openai.log = "debug"
openai.api_key = "sk-"
openai.api_base = "https://api.chatanywhere.com.cn/v1"



# 非流式响应
# completion = openai.ChatCompletion.create(model="gpt-3.5-turbo", messages=[{"role": "user", "content": "Hello world!"}])
# print(completion.choices[0].message.content)

def gpt_35_api_stream(messages: list):
    """为提供的对话消息创建新的回答 (流式传输)

    Args:
        messages (list): 完整的对话消息
        api_key (str): OpenAI API 密钥

    Returns:
        tuple: (results, error_desc)
    """
    try:
        response = openai.ChatCompletion.create(
            model='gpt-3.5-turbo',
            messages=messages,
            stream=True,
        )
        completion = {'role': '', 'content': ''}
        for event in response:
            if event['choices'][0]['finish_reason'] == 'stop':
                print(f'收到的完成数据: {completion}')
                break
            for delta_k, delta_v in event['choices'][0]['delta'].items():
                print(f'流响应数据: {delta_k} = {delta_v}')
                completion[delta_k] += delta_v
        messages.append(completion)  # 直接在传入参数 messages 中追加消息
        return (True, '')
    except Exception as err:
        return (False, f'OpenAI API 异常: {err}')

if __name__ == '__main__':
    messages = [{'role': 'user','content': '鲁迅和周树人的关系'},]
    print(gpt_35_api_stream(messages))
    print(messages)
```