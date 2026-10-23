# Tidal Chronicle · 潮汐纪事

> *Each dawn, lines are cast into the digital deep. What rises — froth, current, or the glint of an unknown truth — is shaped into a message in a bottle, and sent to your shore.*
>
> 每日破晓，向数字深海垂下钓线。浮标震颤的，是浪涌，是暗流，还是深海中无名真理的微光？封入瓶中，托潮汐送至你的岸上。

每日 AI 新闻简报，每天早 8:00 自动抓取四个领域热点 → AI 分析 → 生成日报 → 发送邮件。

## 工作流概览

```
定时触发器 (8:00 AM)
    │
    ├── 时局浮标 (知乎热榜) ────────┐
    ├── 星河浮标 (NewsAPI) ────────┤
    ├── 幻想洋流 (B站热门) ────────┤
    └── AI潮汐 (The Verge RSS)     │
              │                    │
        AI潮汐解析 (JSON→纯文本)   │
              │                    │
              └────────┬───────────┘
                       │
                 消息聚合 (模板拼接)
                    │            │
              哲学之问        时局分析
            (Opus 4.7)      (GPT-5.4)
                 │              │
           深海回响            潮汐索引
         (DS V4 Flash)     (GPT-5.4-mini)
                 │              │
          代码清洗(Python)      │
                 │              │
                 └──────┬───────┘
                        │
                   日报排版 (模板拼接)
                        │
                  LLM清洗 (GPT-5.4-mini)
                        │
                  代码清洗 (Python)
                        │
                 发送邮件 (Outlook ×6)
```

## 板块说明

| 板块 | 说明 | 模型 |
|---|---|---|
| 潮汐索引 | 目录导航，各板块一句话摘要 | GPT-5.4-mini |
| 水面之上 | 四领域新闻深度分析（提取→拆解→推演） | GPT-5.4 |
| 暗涌 | 从新闻中提炼一个抽象哲学命题 | Claude Opus 4.7 |
| 深海回响 | 以海洋神话口吻回答哲学命题 | DeepSeek V4 Flash |

## 需要准备的东西

### 1. Dify 平台

导入 `.yml` 文件到 Dify Workflow。

### 2. API 密钥

| 服务 | 节点 | 获取方式 |
|---|---|---|
| NewsAPI | 星河浮标 | https://newsapi.org/register 免费注册 |
| Anthropic | 哲学之问 | Dify 市场安装 Anthropic 插件，填 API Key |
| OpenAI | 时局分析/潮汐索引/清洗 | Dify 市场安装 OpenAI 插件，填 API Key |
| DeepSeek | 深海回响 | Dify 市场安装 DeepSeek 插件，填 API Key |
| Outlook | 发送邮件 (×6) | Dify 市场安装 Outlook 插件，授权登录 |

### 3. 配置修改

导入后需要把占位符换成真值：

- **星河浮标** → URL 里的 `你的NewsAPI密钥` 换成真的
- **发送消息 / 不正经人 / 鲲鲲酱 / 杰哥 / 老杨 / 温桑** → `你的邮箱@example.com` 换成实际收件人

### 4. 定时触发器

默认每天早上 8:00 (Asia/Shanghai) 执行，可在 Dify 节点里改频率和时间。

## 所需模型

| 模型 | 用途 | 可替代 |
|---|---|---|
| claude-opus-4-7 | 哲学之问 | claude-sonnet-4-6 / 任意推理强的模型 |
| gpt-5.4 | 时局分析 | gpt-5.4-mini / claude-sonnet |
| deepseek-v4-flash | 深海回响 | deepseek-v4-pro / claude-sonnet |
| gpt-5.4-mini | 潮汐索引 / 清洗 | 任意便宜模型 |

## 新闻源

| 来源 | 内容 | 说明 |
|---|---|---|
| 知乎热榜 API | 科技/时局热点 | 无需密钥 |
| B站热门 API | 二次元/娱乐热点 | 无需密钥 |
| NewsAPI (美国头条) | 科技新闻补充 | 需要免费 API Key |
| The Verge AI RSS | AI 行业新闻 | 经 feed2json 转换为 JSON |

### 关于 AI潮汐 的两段式结构

The Verge 的 RSS 是 Atom/XML 格式，Dify 的 HTTP 节点不能直接读。所以拆成两个节点：

1. **AI潮汐** — 请求 `feed2json.org` 把 RSS 转成 JSON Feed
2. **AI潮汐解析** — Python 代码节点抽出标题 / 摘要 / 链接，拼成纯文本

这样改的另一个好处：不依赖 `rss2json` 那类会被 Cloudflare 拦下的服务。想换新闻源时，只改第一个节点的 URL 即可，解析逻辑不用动。

> 注意：文中原用的 `api.rss2json.com` 目前已被 Cloudflare 全站反爬拦截（403 + JS 挑战页），带 UA、走代理都过不去，所以换成了 feed2json。

## 关于「提取 / 拆解 / 推演」

`时局分析` 节点强制模型对每个领域执行三步：先客观提取事实，再把关键方与核心矛盾填空拆开，最后基于文中具体事实推演短期走向。目的是压住模型的评论冲动——只描述「是什么」和「可能发生什么」，不做归因评判。
