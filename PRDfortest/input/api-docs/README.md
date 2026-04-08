# 接口文档目录

此目录用于存放接口文档，供 performance-test-generator skill 使用。

## 支持的文件格式

- JSON 格式（.json）
- YAML 格式（.yaml, .yml）
- Markdown 格式（.md）

## 使用说明

1. 将接口文档放入此目录
2. 确保 `output/requirements/` 目录中存在需求规格说明文档
3. 告诉 Agent："请生成性能测试方案"
4. Agent 将自动读取需求文档和接口文档，生成性能测试方案

## 接口文档示例

### JSON 格式示例

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "API 文档",
    "version": "1.0.0"
  },
  "paths": {
    "/api/login": {
      "post": {
        "summary": "用户登录",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "username": {"type": "string"},
                  "password": {"type": "string"}
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "登录成功"
          }
        }
      }
    }
  }
}
```

### YAML 格式示例

```yaml
openapi: 3.0.0
info:
  title: API 文档
  version: 1.0.0
paths:
  /api/login:
    post:
      summary: 用户登录
      requestBody:
        content:
          application/json:
            schema:
              type: object
              properties:
                username:
                  type: string
                password:
                  type: string
      responses:
        '200':
          description: 登录成功
```

### Markdown 格式示例

```markdown
# API 文档

## 用户登录

- **URL**: `/api/login`
- **Method**: `POST`
- **请求参数**:
  - `username`: 用户名（必填）
  - `password`: 密码（必填）
- **响应**:
  - 200: 登录成功
  - 401: 认证失败
```
