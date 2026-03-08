# Points List API Documentation

## Base URL
```
http://<server-ip>:80
```

## Authentication
Most POST/DELETE endpoints require an API key. The API key is the admin password.

**Header Format:**
```
X-API-Key: <admin_password>
```

Or include in request body:
```json
{
  "api_key": "<admin_password>"
}
```

---

## Player Management APIs

### Get All Players
**Endpoint:** `GET /api/players`

**Response:**
```json
{
  "players": [
    {
      "id": 1,
      "name": "Player Name",
      "score": 12,
      "red_card": false
    }
  ]
}
```

### Add Player
**Endpoint:** `POST /api/players`

**Headers:**
```
X-API-Key: <admin_password>
Content-Type: application/json
```

**Request Body:**
```json
{
  "name": "New Player Name",
  "api_key": "<admin_password>"
}
```

**Response:**
```json
{
  "id": 1,
  "name": "New Player Name",
  "score": 12,
  "red_card": false
}
```

### Remove Player
**Endpoint:** `DELETE /api/players/<player_id>`

**Headers:**
```
X-API-Key: <admin_password>
```

**Response:**
```json
{
  "message": "Player removed"
}
```

### Deduct 3 Points
**Endpoint:** `POST /api/players/<player_id>/deduct`

**Headers:**
```
X-API-Key: <admin_password>
Content-Type: application/json
```

**Request Body:**
```json
{
  "api_key": "<admin_password>"
}
```

**Response:**
```json
{
  "id": 1,
  "name": "Player Name",
  "score": 9,
  "red_card": false
}
```

### Add 3 Points
**Endpoint:** `POST /api/players/<player_id>/add`

**Headers:**
```
X-API-Key: <admin_password>
Content-Type: application/json
```

**Request Body:**
```json
{
  "api_key": "<admin_password>"
}
```

**Response:**
```json
{
  "id": 1,
  "name": "Player Name",
  "score": 12,
  "red_card": false
}
```

### Reset Player Score
**Endpoint:** `POST /api/players/<player_id>/reset`

**Headers:**
```
X-API-Key: <admin_password>
Content-Type: application/json
```

**Request Body:**
```json
{
  "api_key": "<admin_password>"
}
```

**Response:**
```json
{
  "id": 1,
  "name": "Player Name",
  "score": 12,
  "red_card": false
}
```

### Reset All Players
**Endpoint:** `POST /api/players/reset-all`

**Headers:**
```
X-API-Key: <admin_password>
Content-Type: application/json
```

**Request Body:**
```json
{
  "api_key": "<admin_password>"
}
```

**Response:**
```json
{
  "message": "All players reset"
}
```

---

## Admin APIs

### Admin Login
**Endpoint:** `POST /api/admin/login`

**Request Body:**
```json
{
  "password": "admin_password"
}
```

**Response (Success):**
```json
{
  "success": true,
  "api_key": "admin_password"
}
```

**Response (Failure):**
```json
{
  "success": false,
  "message": "Invalid password"
}
```

### Admin Logout
**Endpoint:** `POST /api/admin/logout`

**Response:**
```json
{
  "message": "Logged out"
}
```

### Change Password
**Endpoint:** `POST /api/admin/change-password`

**Headers:**
```
X-API-Key: <current_password>
Content-Type: application/json
```

**Request Body:**
```json
{
  "current_password": "old_password",
  "new_password": "new_password",
  "api_key": "old_password"
}
```

**Response:**
```json
{
  "message": "Password changed successfully"
}
```

---

## Configuration APIs

### Get Configuration
**Endpoint:** `GET /api/config`

**Response:**
```json
{
  "page_title": "Points List",
  "rules": {
    "title": "Scoring Rules",
    "icon": "fa-info-circle",
    "content": "Initial score per person: 12 points\nPlaying games..."
  },
  "footer": "Points List © 2025 | ..."
}
```

---

## Language APIs

### Get Current Language
**Endpoint:** `GET /api/language`

**Response:**
```json
{
  "language": "en",
  "locale": {
    "page_title": "Points List",
    "rules_title": "Scoring Rules",
    ...
  }
}
```

### Set Language
**Endpoint:** `POST /api/language`

**Request Body:**
```json
{
  "language": "zh"
}
```

**Response:**
```json
{
  "message": "Language updated",
  "language": "zh",
  "locale": { ... }
}
```

### Get Language Status
**Endpoint:** `GET /api/language/status`

**Response:**
```json
{
  "set": true,
  "language": "zh"
}
```

---

## Agreement APIs

### Get Agreement Status
**Endpoint:** `GET /api/agreement/status`

**Response:**
```json
{
  "accepted": true
}
```

### Accept Agreement
**Endpoint:** `POST /api/agreement/accept`

**Response:**
```json
{
  "message": "Agreement accepted"
}
```

---

## Error Responses

### 400 Bad Request
```json
{
  "error": "Missing required field"
}
```

### 401 Unauthorized
```json
{
  "error": "Invalid or missing API key"
}
```

### 404 Not Found
```json
{
  "error": "Player not found"
}
```

---

## Example Usage

### cURL Examples

**Get all players:**
```bash
curl http://192.168.31.88:5001/api/players
```

**Add player:**
```bash
curl -X POST http://192.168.31.88:5001/api/players \
  -H "Content-Type: application/json" \
  -H "X-API-Key: admin123" \
  -d '{"name": "John Doe"}'
```

**Deduct points:**
```bash
curl -X POST http://192.168.31.88:5001/api/players/1/deduct \
  -H "Content-Type: application/json" \
  -H "X-API-Key: admin123" \
  -d '{"api_key": "admin123"}'
```

**Set language to Chinese:**
```bash
curl -X POST http://192.168.31.88:5001/api/language \
  -H "Content-Type: application/json" \
  -d '{"language": "zh"}'
```

---

## Data Persistence

All data is stored in JSON files:
- `students_data.json` - Player data
- `config.json` - System configuration
- `locales.json` - Language translations

Data is automatically saved after every modification.

---

---

# Points List API 文档（中文版）

## 基础 URL
```
http://<服务器IP>:80
```

## 认证方式
大多数 POST/DELETE 接口需要 API 密钥。API 密钥即管理员密码。

**请求头格式：**
```
X-API-Key: <admin_password>
```

或在请求体中包含：
```json
{
  "api_key": "<admin_password>"
}
```

---

## 人员管理接口

### 获取所有人员
**接口：** `GET /api/players`

**响应：**
```json
{
  "players": [
    {
      "id": 1,
      "name": "人员姓名",
      "score": 12,
      "red_card": false
    }
  ]
}
```

### 添加人员
**接口：** `POST /api/players`

**请求头：**
```
X-API-Key: <admin_password>
Content-Type: application/json
```

**请求体：**
```json
{
  "name": "新人员姓名",
  "api_key": "<admin_password>"
}
```

**响应：**
```json
{
  "id": 1,
  "name": "新人员姓名",
  "score": 12,
  "red_card": false
}
```

### 移除人员
**接口：** `DELETE /api/players/<player_id>`

**请求头：**
```
X-API-Key: <admin_password>
```

**响应：**
```json
{
  "message": "Player removed"
}
```

### 扣3分
**接口：** `POST /api/players/<player_id>/deduct`

**请求头：**
```
X-API-Key: <admin_password>
Content-Type: application/json
```

**请求体：**
```json
{
  "api_key": "<admin_password>"
}
```

**响应：**
```json
{
  "id": 1,
  "name": "人员姓名",
  "score": 9,
  "red_card": false
}
```

### 加3分
**接口：** `POST /api/players/<player_id>/add`

**请求头：**
```
X-API-Key: <admin_password>
Content-Type: application/json
```

**请求体：**
```json
{
  "api_key": "<admin_password>"
}
```

**响应：**
```json
{
  "id": 1,
  "name": "人员姓名",
  "score": 12,
  "red_card": false
}
```

### 重置人员分数
**接口：** `POST /api/players/<player_id>/reset`

**请求头：**
```
X-API-Key: <admin_password>
Content-Type: application/json
```

**请求体：**
```json
{
  "api_key": "<admin_password>"
}
```

**响应：**
```json
{
  "id": 1,
  "name": "人员姓名",
  "score": 12,
  "red_card": false
}
```

### 重置所有人员
**接口：** `POST /api/players/reset-all`

**请求头：**
```
X-API-Key: <admin_password>
Content-Type: application/json
```

**请求体：**
```json
{
  "api_key": "<admin_password>"
}
```

**响应：**
```json
{
  "message": "All players reset"
}
```

---

## 管理员接口

### 管理员登录
**接口：** `POST /api/admin/login`

**请求体：**
```json
{
  "password": "admin_password"
}
```

**响应（成功）：**
```json
{
  "success": true,
  "api_key": "admin_password"
}
```

**响应（失败）：**
```json
{
  "success": false,
  "message": "Invalid password"
}
```

### 管理员登出
**接口：** `POST /api/admin/logout`

**响应：**
```json
{
  "message": "Logged out"
}
```

### 修改密码
**接口：** `POST /api/admin/change-password`

**请求头：**
```
X-API-Key: <current_password>
Content-Type: application/json
```

**请求体：**
```json
{
  "current_password": "old_password",
  "new_password": "new_password",
  "api_key": "old_password"
}
```

**响应：**
```json
{
  "message": "Password changed successfully"
}
```

---

## 配置接口

### 获取配置
**接口：** `GET /api/config`

**响应：**
```json
{
  "page_title": "Points List",
  "rules": {
    "title": "Scoring Rules",
    "icon": "fa-info-circle",
    "content": "Initial score per person: 12 points\nPlaying games..."
  },
  "footer": "Points List © 2025 | ..."
}
```

---

## 语言接口

### 获取当前语言
**接口：** `GET /api/language`

**响应：**
```json
{
  "language": "en",
  "locale": {
    "page_title": "Points List",
    "rules_title": "Scoring Rules",
    ...
  }
}
```

### 设置语言
**接口：** `POST /api/language`

**请求体：**
```json
{
  "language": "zh"
}
```

**响应：**
```json
{
  "message": "Language updated",
  "language": "zh",
  "locale": { ... }
}
```

### 获取语言状态
**接口：** `GET /api/language/status`

**响应：**
```json
{
  "set": true,
  "language": "zh"
}
```

---

## 用户协议接口

### 获取协议状态
**接口：** `GET /api/agreement/status`

**响应：**
```json
{
  "accepted": true
}
```

### 接受协议
**接口：** `POST /api/agreement/accept`

**响应：**
```json
{
  "message": "Agreement accepted"
}
```

---

## 错误响应

### 400 错误请求
```json
{
  "error": "Missing required field"
}
```

### 401 未授权
```json
{
  "error": "Invalid or missing API key"
}
```

### 404 未找到
```json
{
  "error": "Player not found"
}
```

---

## 使用示例

### cURL 示例

**获取所有人员：**
```bash
curl http://192.168.31.88:5001/api/players
```

**添加人员：**
```bash
curl -X POST http://192.168.31.88:5001/api/players \
  -H "Content-Type: application/json" \
  -H "X-API-Key: admin123" \
  -d '{"name": "张三"}'
```

**扣分：**
```bash
curl -X POST http://192.168.31.88:5001/api/players/1/deduct \
  -H "Content-Type: application/json" \
  -H "X-API-Key: admin123" \
  -d '{"api_key": "admin123"}'
```

**设置中文：**
```bash
curl -X POST http://192.168.31.88:5001/api/language \
  -H "Content-Type: application/json" \
  -d '{"language": "zh"}'
```

---

## 数据持久化

所有数据存储在 JSON 文件中：
- `students_data.json` - 人员数据
- `config.json` - 系统配置
- `locales.json` - 语言翻译

每次修改后数据会自动保存。
