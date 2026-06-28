# Tidal Chronicle · 潮汐纪事

> *Each dawn, lines are cast into the digital deep. What rises — froth, current, or the glint of an unknown truth — is shaped into a message in a bottle, and sent to your shore.*
>
> 每日破晓，向数字深海垂下钓线。浮标震颤的，是浪涌，是暗流，还是深海中无名真理的微光？封入瓶中，托潮汐送至你的岸上。

An automated daily briefing engine on Dify. Four data streams → triple distillation → a clean newsletter in your inbox.

---

## What is this

A Dify workflow that wakes at 08:00 daily, fishes signals from four waters, distills them through three layers — **rational analysis → philosophical condensation → abyssal echo** — and delivers a judgement-free briefing to your email.

---

## Pipeline

```
Daily 08:00 (Asia/Shanghai)
    │
    ├─ 时局浮标 (Zhihu) ────┐
    ├─ AI 潮汐  (Verge AI) ─┤
    ├─ 幻想洋流 (Bilibili) ─┤  Four hooks drop
    └─ 星河浮标 (NewsAPI)  ─┘  simultaneously
              │
              ▼
         Aggregation
              │
       ┌──────┴──────┐
       ▼              ▼
  Philosophical       Analysis
  Question (Claude)   (GPT-5.4)
  One abstract        Extract → dissect
  question pulled     → project.
  from the surface.   Facts only.
       │              │
       ▼              │
  Abyssal Echo         │
  (DeepSeek)            │
  Poetic answer         │
  from the deep.        │
       │              │
       ▼              │
  Strip <think>        │
  (Python)             │
       │              │
       └──────┬───────┘
              ▼
           Layout
  Above Surface / Undercurrent
        / Abyssal Echo
              │
              ▼
       LLM Polish (GPT-4o-mini)
    Remove step labels & markdown
              │
              ▼
       Deep Clean (Python)
    Crush residual <think> & self-talk
    < 50 chars → "The tide is calm today."
              │
              ▼
    📧 Bottle delivered (Outlook)
```

---

## Data Sources

| Buoy | Waters | Bait |
|------|--------|------|
| 时局浮标 | Zhihu hot list | Sociopolitical pulses |
| AI 潮汐 | The Verge AI (rss2json) | Human-machine ripples |
| 幻想洋流 | Bilibili popular videos | ACG emotional currents |
| 星河浮标 | NewsAPI US headlines | Tech & world surface signals |

星河浮标 requires a [NewsAPI](https://newsapi.org) key (free for personal use).

---

## Setup

1. **Import** `潮汐纪事.yml` into Dify (workflow mode, 0.6.0+)
2. **Set key** — replace `YOUR_NEWSAPI_KEY` in the 星河浮标 node URL
3. **Pick models** — select available models in LLM nodes (Anthropic / OpenAI / DeepSeek)
4. **Bind email** — Outlook authorization in the send node → replace recipient address
5. **(Optional)** Adjust schedule trigger (default 08:00)
6. **Test** — manually trigger once to verify the bottle arrives

---

## Three Sections

| Section | Meaning |
|---------|---------|
| 水面之上 (Above Surface) | Today's observable signals |
| 暗涌 (Undercurrent) | The philosophical question distilled from the noise |
| 深海回响 (Abyssal Echo) | The poetic answer from the deep |

If the final text is too short, only a quiet note from the abyss remains. That is not a bug — the ocean chose silence today.

---

## Dependencies

Dify 0.6.0+ · Anthropic · OpenAI · DeepSeek · Outlook · NewsAPI

---

## 这是什么

一座 Dify 自动化日志引擎。每天 08:00 从四个海域打捞今日信号，经三重蒸馏——**理性拆解 → 哲学凝练 → 深海回响**——炼成无评判纯净日报投递到邮箱。

---

## 流程

```
每日 08:00
    │
    ├─ 时局浮标 (知乎)    ──┐
    ├─ AI 潮汐  (Verge)    ─┤
    ├─ 幻想洋流 (B 站)     ─┤  四线同时下钩
    └─ 星河浮标 (NewsAPI)  ─┘
              │
              ▼
          消息聚合
              │
       ┌──────┴──────┐
       ▼              ▼
  哲学之问          时局分析
  (Claude)          (GPT-5.4)
  提炼一个抽象      提取→拆解→推演
  哲学命题          纯事实无评判
       │              │
       ▼              │
  深海回响             │
  (DeepSeek)           │
  诗意回应哲学之问      │
       │              │
       ▼              │
  去除 <think>         │
  (Python)            │
       │              │
       └──────┬───────┘
              ▼
         日报排版
   水面之上 / 暗涌 / 深海回响
              │
              ▼
      LLM 净化 (GPT-4o-mini)
   扫去步骤标签与 Markdown 引导语
              │
              ▼
       代码深度清洗 (Python)
   碾碎残留 <think> 与自我对话
   净文 < 50 字符 → "今日潮汐未至"
              │
              ▼
    📧 漂流瓶投递 (Outlook)
```

---

## 数据源

| 浮标 | 海域 | 饵料 |
|------|------|------|
| 时局浮标 | 知乎热榜 | 社会 & 政经脉冲 |
| AI 潮汐 | The Verge AI (rss2json) | 人机交汇涟漪 |
| 幻想洋流 | B 站热门视频 | ACG 情绪对流 |
| 星河浮标 | NewsAPI 美国头条 | 科技 & 世界表层信号 |

星河浮标需 [NewsAPI](https://newsapi.org) 密钥（免费版仅供个人使用）。

---

## 部署

1. **导入** `潮汐纪事.yml` → Dify（workflow 模式，需 0.6.0+）
2. **填钥** — 星河浮标节点 URL 中替换 `YOUR_NEWSAPI_KEY`
3. **选模** — LLM 节点指定可用模型（Anthropic / OpenAI / DeepSeek）
4. **绑箱** — Outlook 授权 → 替换收件人地址
5. **（可选）** 调定时触发器（默认 08:00）
6. **试钓** — 手动触发一次确认抵达

---

## 三版块

| 版块 | 释义 |
|------|------|
| 水面之上 | 当日可观测的现实信号 |
| 暗涌 | 从信号中提炼的哲学之问 |
| 深海回响 | 以诗意回应的未知之答 |

若净文过短仅剩一句深海告示——那不是故障，是海洋今日选择了沉默。

---

## 依赖

Dify 0.6.0+ · Anthropic · OpenAI · DeepSeek · Outlook · NewsAPI
