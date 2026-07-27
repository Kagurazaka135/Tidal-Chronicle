# Tidal Chronicle · 潮汐纪事

> *Each dawn, lines are cast into the digital deep. What rises — froth, current, or the glint of an unknown truth — is shaped into a message in a bottle, and sent to your shore.*
>
> 每日破晓，向数字深海垂下钓线。浮标震颤的，是浪涌，是暗流，还是深海中无名真理的微光？封入瓶中，托潮汐送至你的岸上。

每日 AI 新闻简报，每天早 8:00 自动抓取四个领域热点 → AI 分析 → 生成日报 → 发送邮件。

## 工作流概览

```
定时触发器 (8:00 AM)
    │
    ├── 时局浮标 (知乎热榜)
    ├── AI潮汐 (The Verge RSS)
    ├── 幻想洋流 (B站热门)
    ├── 星河浮标 (NewsAPI)
    └── 风色观测 (彩云天气)
           │
     消息聚合 (模板拼接)
           │
     ┌─────┼─────┬──────────┐
     │     │     │          │
  哲学之问 时局分析 天象浮标   潮汐索引
  (Sonnet) (GPT5.4)(GPT mini)(GPT mini)
     │     │     │          │
     │     │     └────┬─────┘
     │     │          │
     └──┬──┘    日报排版 (模板拼接)
        │          │
     深海回响   LLM清洗 (GPT mini)
     (DS V4)      │
        │     代码清洗 (Python)
        └─────┬──┘
              │
          发送邮件 (Outlook ×3)
```

## 板块说明

| 板块 | 说明 | 模型 |
|---|---|---|
| 潮汐索引 | 目录导航，各板块一句话摘要 | GPT-4o-mini |
| 天象浮标 | 天气 + 出门注意事项 | GPT-4o-mini |
| 水面之上 | 四领域新闻深度分析（提取→拆解→推演） | GPT-5.4 |
| 暗涌 | 从新闻中提炼一个抽象哲学命题 | Claude Sonnet 4.6 |
| 深海回响 | 以海洋神话口吻回答哲学命题 | DeepSeek V4 Pro |

## 需要准备的东西

### 1. Dify 平台

导入 `.yml` 文件到 Dify Workflow。

### 2. API 密钥

| 服务 | 节点 | 获取方式 |
|---|---|---|
| 彩云天气 | 风色观测 | https://dashboard.caiyunapp.com 免费注册 |
| NewsAPI | 星河浮标 | https://newsapi.org/register 免费注册 |
| Anthropic | 哲学之问 | Dify 市场安装 Anthropic 插件，填 API Key |
| OpenAI | 时局分析/天象浮标/潮汐索引/清洗 | Dify 市场安装 OpenAI 插件，填 API Key |
| DeepSeek | 深海回响 | Dify 市场安装 DeepSeek 插件，填 API Key |
| Outlook | 发送邮件 (×3) | Dify 市场安装 Outlook 插件，授权登录 |

### 3. 配置修改

导入后需要改这些地方：

- **风色观测** → URL 里的 `你的彩云天气API密钥` 换成真的
- **星河浮标** → URL 里的 `你的NewsAPI密钥` 换成真的
- **发送消息 / 不正经人 / 鲲鲲酱** → `收件人` 换成实际邮箱
- 天气坐标默认成都 (104.0671, 30.4098)，要换城市去彩云天气改

### 4. 定时触发器

默认每天早上 8:00 (Asia/Shanghai) 执行，可在 Dify 节点里改频率和时间。

## 所需模型

| 模型 | 用途 | 可替代 |
|---|---|---|
| claude-sonnet-4-6 | 哲学之问 | 任意推理能力强的模型 |
| gpt-5.4 | 时局分析 | gpt-4o / claude-sonnet |
| deepseek-v4-pro | 深海回响 | claude-sonnet / gpt-5.4 |
| gpt-4o-mini | 天象浮标 / 潮汐索引 / 清洗 | 任意便宜模型 |

## 新闻源

| 来源 | 内容 |
|---|---|
| 知乎热榜 API | 科技/时局热点 |
| The Verge AI RSS | AI 行业新闻 |
| B站热门 API | 二次元/娱乐热点 |
| NewsAPI (美国头条) | 科技新闻补充 |

知乎和 B站 API 不需要密钥，直接用。
