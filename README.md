
### 题库内容
**支持各大网课的题目答案查询，超星，智慧树，知到，Welearn等各种网课免费使用，支持OCS网课助手脚本对接**

#### 支持模糊搜索！！（输入部分题目即可搜索到答案）

## 免费token:qqqqq

### API对接方法
```
http://api.wkexam.com/api/?token=你的token&q=你的问题
```
### OCS网课助手对接代码
```
[
    {
        "name": "网课考试题库",
        "url": "https://api.wkexam.com/api/",
        "method": "get",
        "type": "GM_xmlhttpRequest",
        "data": {
            "q": "${title}",
            "token": "替换为你的token"
        },
        "handler": "return (res)=> res.code === 1 ? [res.data.question,res.data.answer] :[res.message || '请求失败', undefined]"
    }
]
```
### 请求参数

| 参数名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| token | string | 是 | 访问令牌 |
| q | string | 是 | 搜索的题目内容 |
| options | array | 否 | 选项内容（选填） |

### 响应格式

#### 成功响应

```json
{
    "code": 1,
    "data": {
        "question": "题目内容",
        "answer": "答案内容"
    },
    "message": "请求成功"
}
```

#### 失败响应

```json
{
    "code": 0,
    "data": {
        "question": "搜索的题目内容",
        "answer": "错误提示信息"
    },
    "message": "请求失败：具体原因"
}
```

### 响应参数说明

| 参数名 | 类型 | 说明 |
|--------|------|------|
| code | int | 响应状态码，1=成功，0=失败 |
| data | object | 响应数据对象 |
| data.question | string | 题目内容 |
| data.answer | string | 答案内容或错误提示 |
| message | string | 响应消息说明 |

### 错误码说明

| 错误情况 | 返回消息 |
|----------|----------|
| 题目为空 | 题目内容不能为空 |
| token为空 | token不能为空 |
| token无效 | token无效 |
| token被禁用 | 该token已被禁用 |
| 超出使用限制 | 已达到每日使用限制 (N次) |
| 未找到答案 | 题目搜索不到 |
| 服务器错误 | 服务器内部错误 |

### 请求示例

```bash
curl -X GET "http://api.wkexam.com/api/?token=qqqqq&q=中国梦是什么？"
```

### 响应示例

#### 成功响应示例

```json
{
    "code": 1,
    "data": {
        "question": "以下错误描述人对事物的好恶的是()。",
        "answer": "人的好恶是无法被自身控制的"
    },
    "message": "请求成功"
}
```

#### 失败响应示例

```json
{
    "code": 0,
    "data": {
        "question": "以下错误描述人对事物的好恶的是()。",
        "answer": "很抱歉, token已达到每日使用限制 (1000次)"
    },
    "message": "请求失败：已达到每日使用限制 (1000次)"
}
```


