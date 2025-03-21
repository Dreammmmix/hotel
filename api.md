
# API KEY:8b37c4be-9619-4514-b99e-fc7ffb0e39f4

# API调用示例

```python
import os
from openai import OpenAI

client = OpenAI(
    api_key = os.environ.get("ARK_API_KEY"),
    base_url = "https://ark.cn-beijing.volces.com/api/v3",
)

# Non-streaming:
print("----- standard request -----")
completion = client.chat.completions.create(
    model = "deepseek-r1-250120",  # your model endpoint ID
    messages = [
        {"role": "system", "content": "你是人工智能助手"},
        {"role": "user", "content": "常见的十字花科植物有哪些？"},
    ],
)
print(completion.choices[0].message.content)

# Streaming:
print("----- streaming request -----")
stream = client.chat.completions.create(
    model = "deepseek-r1-250120",  # your model endpoint ID
    messages = [
        {"role": "system", "content": "你是人工智能助手"},
        {"role": "user", "content": "常见的十字花科植物有哪些？"},
    ],
    stream=True
)

for chunk in stream:
    if not chunk.choices:
        continue
    print(chunk.choices[0].delta.content, end="")
print()
```