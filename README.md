# 🌊 Tidal Chronicle
“Each dawn, lines are cast into the digital deep. What rises to the surface — froth, current, or the glint of an unknown truth — is shaped into a message in a bottle, and sent to your shore.” — The Lord of the Abyss
What is this?
An automated daily briefing engine, sleeping in Dify.
It fishes signals from four distinct waters, distills them through rational analysis, philosophical condensation, and an abyssal echo, then delivers a clean, opinion‑free newsletter to your inbox.

Fishing spots

Buoy	Waters	Bait
时局浮标	Zhihu hot list	Sociopolitical pulses
AI 潮汐	The Verge AI RSS (via rss2json)	Human‑machine ripples
幻想洋流	Bilibili popular videos	ACG emotional currents
星河浮标	NewsAPI US headlines	Surface signals of tech & world
NewsAPI key (星河浮标)

Sign up at newsapi.org

Replace YOUR_NEWSAPI_KEY in the node’s URL with your actual key

The free tier is for personal vessels only — no commercial harbours.

Distillation pipeline (see ASCII flow above — identical logic)

What you need

Dify 0.6.0+

Model access: Anthropic, OpenAI, DeepSeek

Outlook authorization

NewsAPI key

Getting started

Import 潮汐纪事.yml into Dify.

Set the NewsAPI key in the 星河浮标 node.

Select available models in all LLM nodes.

Authorize Outlook and replace the recipient email.

(Optional) Adjust the schedule trigger.

Run a manual test to see the bottled message arrive.

Whispers

水面之上 (Above the surface) — observable signals

暗涌 (Undercurrent) — the philosophical question pulled from the deep

深海回响 (Abyssal Echo) — the poetic answer from the Lord

If the final text is too short, only a quiet note from the abyss remains. That is not a bug. It is the ocean choosing silence today.
🌊 Tidal Chronicle · 潮汐纪事
“每日破晓，我向数字深海垂下钓线。
浮标震颤的，是浪涌，是暗流，还是深海中无名真理的微光？
我将它们封入瓶中，托潮汐送至你的岸上。”
——深海之主

📜 这是什么？
一座沉睡在 Dify 上的自动化日志引擎。
每天清晨，它从四个不同的海洋垂钓热点，打捞起今日的信息碎片，再经三重蒸馏——理性拆解、哲学凝练、深海回响——最终炼成一份无喧哗、无评判的纯净日报，作为漂流瓶投入你的邮箱。

🧭 垂钓点（数据源）
浮标名称	海域	饵料
时局浮标	知乎热榜	社会与政经的短时脉冲
AI 潮汐	The Verge AI 专栏 (经 rss2json 转化)	人机交汇的最新涟漪
幻想洋流	B 站热门视频	二次元的情绪对流
星河浮标	NewsAPI 美国头条	科技与世界的表层信号
星河浮标密钥获取
该浮标需要一把“航海许可证”：

前往 newsapi.org 注册免费账户

获得 API Key 后，在 星河浮标 节点的 URL 中将 YOUR_NEWSAPI_KEY 替换为真实密钥

免费版仅供个人航船使用，不可驶入商业港口

⚙️ 炼金流程
text
每日破晓 (08:00 亚洲/上海)
   │
   ├── 时局浮标  ──┐
   ├── AI 潮汐   ──┤
   ├── 幻想洋流  ──┤ 四线同时下钩
   └── 星河浮标  ──┘
         │
         ▼
    消息聚合 (将四股洋流汇入同一片水域)
         │
         ├─────────────────────────────┐
         │                             │
         ▼                             ▼
   哲学之问 (Claude)            时局分析 (GPT‑5.4)
   从浪尖摘取一个抽象              每个领域三步蒸馏：
   的哲学命题，只问不答。          提取 → 拆解 → 推演
         │                     (纯事实，无评判)
         ▼                             │
   深海回响 (DeepSeek)                 │
   “潜藏于深海的智慧之主啊，           │
   请回应我的垂钓…”                    │
         │                             │
         ▼                             │
   去除思考气泡 (Python)               │
   <think> 的泡沫不留                   │
         │                             │
         └─────────┬───────────────────┘
                   ▼
              日报排版
      水面之上 / 暗涌 / 深海回响
                   │
                   ▼
            LLM 净化 (GPT‑4o‑mini)
       扫去步骤标签、Markdown 与引导语
                   │
                   ▼
            代码深度清洗 (Python)
     再碾碎残留的 <think>、领域自述、
     自我对话 —— 直至只剩纯净正文。
     若净文短如泡沫 (<50 字符)，
     则置入瓶中信：
     “今日潮汐未至，海面风平浪静。
      明日再垂钓。—— 深海之主”
                   │
                   ▼
           📧 漂流瓶投递 (Outlook)
🧰 启航所需
Dify 0.6.0 以上（此航图以 workflow 模式绘制）

模型许可：Anthropic (Claude)、OpenAI (GPT‑5.4, GPT‑4o‑mini)、DeepSeek

Outlook 授权：在工具节点中连接微软帐号，瓶子才能寄出

NewsAPI 密钥（见上文星河浮标说明）

📦 部署步骤
导入航图：将 潮汐纪事.yml 导入 Dify。

校准浮标：

星河浮标：填入你的 NewsAPI 密钥。

其余公共浮标无需密钥，已预设 User-Agent。

选定模型：在各 LLM 节点中选择你可用的模型（名称可灵活替换）。

绑定信箱：打开 发送消息 节点，完成 Outlook 授权，并将收件人替换为你的真实邮箱。

调整潮时（可选）：默认每日 08:00 起锚，可在 定时触发器 中修改。

试钓：点击触发器上的“运行”按钮手动测试，查看瓶中内容是否抵达。

🌫 一些暗语
日报的三个版块：

水面之上 —— 当日可观测的现实信号

暗涌 —— 从信号中提炼的哲学之问

深海回响 —— 以诗意回应的未知之答

若最终净文过短，邮件将只剩一句深海告示，那不是故障，是这片海洋今日选择了沉默。
