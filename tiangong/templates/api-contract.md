# 接口约定

> 模板：每个接口一节（或一文件），放入 docs/contracts/。未写明的行为不得各自猜测。

## <接口名>（例：评测机取下一题）

- 路径与方法：`GET /api/judge/next`
- 身份：`Authorization: Bearer <token>`（无登录则删此行）
- 分页（若有）：`?page=1&size=20`

### 成功一例

请求：

```text
GET /api/judge/next
Authorization: Bearer <token>
```

响应 `200`：

```json
{ "task_id": "t-1001", "language": "cpp" }
```

### 常见失败一例

响应 `204`：（当前无任务）

### 临时假实现

- [ ] 若本接口为固定返回值顶替：在此打勾，写明位置，并写明**第几阶段替换为真实实现**
