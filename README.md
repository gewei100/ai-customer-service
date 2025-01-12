# AI Customer Service Assistant

基于 React 和 OpenAI 打造的智能客服助手，支持知识库问答和 URL 内容解析。

[![React](https://img.shields.io/badge/React-18.x-blue)](https://reactjs.org/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-green)](https://openai.com/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## 功能特点

- 🤖 智能问答：基于 OpenAI GPT-4 的智能回答
- 📚 知识库集成：支持自定义知识库内容
- 🔗 URL 解析：可解析网页内容作为回答依据
- 💬 实时对话：流畅的对话式交互体验
- 🎨 美观界面：基于 shadcn/ui 的现代化设计

## 安装部署

### 环境要求

- Node.js >= 16.0.0
- React >= 18.0.0
- shadcn/ui 组件库

### 基础安装

```bash
# 克隆项目
git clone https://github.com/your-username/ai-customer-service.git

# 安装依赖
cd ai-customer-service
npm install

# 安装 shadcn/ui 组件
npx shadcn-ui@latest init
npx shadcn-ui@latest add card
```

### 环境配置

1. 在项目根目录创建 `.env` 文件：

```env
OPENAI_KEY=your_openai_api_key
OPENAI_BASE_URL=https://api.openai.com/v1
```

2. 配置知识库内容（可选）：
编辑 `src/data/knowledgeBase.js`：

```javascript
export const documentContent = `
# 您的文档内容
## 章节一
内容...
`;
```

## 使用方法

### 基础用法

```javascript
import { AIAssistant } from './components/AIAssistant';

function App() {
  return (
    <div>
      <AIAssistant />
    </div>
  );
}
```

### 组件属性

| 属性名 | 类型 | 默认值 | 说明 |
|--------|------|--------|------|
| theme | string | 'light' | 主题样式 |
| customStyles | object | {} | 自定义样式 |
| onMessage | function | undefined | 消息回调函数 |

### 示例代码

```javascript
<AIAssistant
  theme="dark"
  customStyles={{ maxWidth: '800px' }}
  onMessage={(msg) => console.log('New message:', msg)}
/>
```

## API 文档

### URL 内容获取

```javascript
POST /api/fetch-url
Content-Type: application/json

{
  "url": "https://example.com/document"
}
```

### OpenAI 调用

```javascript
POST /chat/completions
Headers: {
  'Authorization': `Bearer ${OPENAI_KEY}`,
  'Content-Type': 'application/json'
}

{
  "model": "gpt-4-turbo-preview",
  "messages": [
    {
      "role": "system",
      "content": "系统提示..."
    },
    {
      "role": "user",
      "content": "用户问题..."
    }
  ]
}
```

## 自定义开发

### 扩展知识库

1. 创建知识库文件：

```javascript
// src/data/customKnowledge.js
export const customContent = `
您的自定义内容...
`;
```

2. 导入并使用：

```javascript
import { customContent } from './data/customKnowledge';

// 在 AIAssistant 组件中使用
const documentContent = customContent;
```

### 样式定制

组件使用 Tailwind CSS 进行样式管理，您可以通过以下方式自定义：

1. 修改默认主题：
```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: {...},
        secondary: {...}
      }
    }
  }
}
```

2. 添加自定义样式类：
```javascript
<div className="your-custom-class">
  <AIAssistant />
</div>
```

## 常见问题

### Q: 如何更改 API 请求超时时间？

在 fetch 请求中添加 timeout 选项：

```javascript
const fetchUrlContent = async (url) => {
  const controller = new AbortController();
  const timeout = setTimeout(() => controller.abort(), 5000);
  
  try {
    const response = await fetch(url, {
      signal: controller.signal
    });
    // ...
  } finally {
    clearTimeout(timeout);
  }
};
```

### Q: 如何处理大量并发请求？

实施请求队列和节流控制：

```javascript
import { throttle } from 'lodash';

const throttledRequest = throttle(async (url) => {
  // 请求处理逻辑
}, 1000);
```

## 贡献指南

1. Fork 本仓库
2. 创建特性分支：`git checkout -b feature/AmazingFeature`
3. 提交改动：`git commit -m 'Add AmazingFeature'`
4. 推送分支：`git push origin feature/AmazingFeature`
5. 提交 Pull Request

## 许可证

本项目使用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

## 联系方式

- 项目作者：Your Name
- Email：your.email@example.com
- GitHub：[@your-username](https://github.com/your-username)
