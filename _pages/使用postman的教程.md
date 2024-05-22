---
title: "使用postman的教程"
tags:
    - postman
    - requests
    - http
date: "2024-05-22"
bookmark: true
thumbnail: "/assets/img/thumbnail/postman.webp"
---

# 使用 Postman 的教程

Postman 是一个流行的 API 客户端，可以帮助开发人员轻松地创建、测试和管理 API 请求。本文将介绍如何使用 Postman 发送请求、组织请求集、使用环境变量，以及其他一些高级功能。

## 安装 Postman

1. **下载 Postman**

   访问 [Postman 官方网站](https://www.postman.com/downloads/) 下载适用于你操作系统的 Postman 客户端。

2. **安装 Postman**

   下载完成后，按照安装向导安装 Postman。

## 基本使用

### 发送一个简单的 GET 请求

1. **启动 Postman**

   打开 Postman 客户端。

2. **创建新请求**

   点击左上角的 `New` 按钮，然后选择 `Request`。

3. **设置请求方法和 URL**

   在请求方法下拉菜单中选择 `GET`，然后在输入框中输入目标 URL，例如 `https://jsonplaceholder.typicode.com/posts`。

4. **发送请求**

   点击 `Send` 按钮。你会在下方看到请求的响应数据。

### 发送 POST 请求

1. **创建新请求**

   同样，点击 `New` 按钮并选择 `Request`。

2. **设置请求方法和 URL**

   在请求方法下拉菜单中选择 `POST`，然后输入目标 URL，例如 `https://jsonplaceholder.typicode.com/posts`。

3. **设置请求头**

   在 `Headers` 选项卡中添加请求头，键为 `Content-Type`，值为 `application/json`。

4. **设置请求体**

   在 `Body` 选项卡中选择 `raw`，并确保选择 `JSON` 格式。在文本框中输入 JSON 数据，例如：

   ```json
   {
     "title": "foo",
     "body": "bar",
     "userId": 1
   }
   ```

5. **发送请求**

   点击 `Send` 按钮。你会在下方看到请求的响应数据。

## 组织请求集

### 创建新的 Collection

1. **创建 Collection**

   在左侧栏点击 `Collections` 标签，然后点击 `New Collection` 按钮。

2. **添加请求到 Collection**

   在新建请求时，将请求保存到指定的 Collection 中，或在请求的 `Save` 按钮旁边选择 `Add to Collection`。

### 导出和导入 Collection

1. **导出 Collection**

   右键点击你创建的 Collection，选择 `Export`，然后选择导出格式（通常选择默认的 JSON 格式）。

2. **导入 Collection**

   点击左上角的 `Import` 按钮，选择 `Upload Files`，然后选择你导出的 JSON 文件。

## 使用环境变量

### 创建环境变量

1. **打开环境管理器**

   点击右上角的齿轮图标，选择 `Manage Environments`。

2. **创建新环境**

   点击 `Add` 按钮，为新环境命名并添加变量。例如，添加一个变量 `baseUrl`，值为 `https://jsonplaceholder.typicode.com`。

3. **使用环境变量**

   在请求 URL 中使用环境变量，格式为 `{{variable_name}}`，例如：

   ```
   {{baseUrl}}/posts
   ```

4. **切换环境**

   在右上角的环境切换器中选择你创建的环境。

## 高级功能

### 使用测试和断言

Postman 提供了强大的测试和断言功能，可以在请求后自动执行脚本来验证响应。

1. **添加测试**

   在请求的 `Tests` 选项卡中添加 JavaScript 代码。例如，检查响应状态码是否为 200：

   ```javascript
   pm.test("Status code is 200", function () {
     pm.response.to.have.status(200);
   });
   ```

2. **运行测试**

   发送请求后，切换到 `Tests` 选项卡查看测试结果。

### 使用 Pre-request Script

你可以在请求发送之前执行脚本，通常用于设置或修改环境变量。

1. **添加 Pre-request Script**

   在请求的 `Pre-request Script` 选项卡中添加 JavaScript 代码。例如，设置当前时间戳为环境变量：

   ```javascript
   pm.environment.set("currentTimestamp", new Date().toISOString());
   ```

### 使用 Postman Runner

Postman Runner 可以批量运行 Collection 中的请求，适用于测试 API 流程和回归测试。

1. **打开 Postman Runner**

   点击左上角的 `Runner` 按钮。

2. **选择 Collection 和环境**

   在 Postman Runner 界面中选择你要运行的 Collection 和对应的环境。

3. **运行 Collection**

   点击 `Start Run` 按钮，查看每个请求的执行结果和测试情况。

## 总结

通过本文，你已经学习了如何安装和使用 Postman 发送请求、组织请求集、使用环境变量，以及一些高级功能。Postman 是一个功能强大的工具，能够大大简化 API 开发和测试工作。

---

如果你在使用过程中遇到问题，可以参考 Postman 的[官方文档](https://learning.postman.com/docs/getting-started/introduction/)或在社区寻求帮助。