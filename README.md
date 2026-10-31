<div align="center">

# 🧠 DS/ML Engineering Skills

### The Universal AI Skill Pack for Data Scientists, ML Engineers & Analysts

**10 battle-tested skills** that turn any AI model (**ChatGPT, Claude, Gemini, Cursor, Antigravity**) into a disciplined, senior Data Science & ML Engineering partner.

[![Skills](https://img.shields.io/badge/Skills-10-blueviolet?style=for-the-badge)]()
[![Roles](https://img.shields.io/badge/Roles-Data_Scientist_·_ML_Engineer_·_Data_Analyst-blue?style=for-the-badge)]()
[![Platforms](https://img.shields.io/badge/Platforms-ChatGPT_·_Claude_·_Gemini_·_Cursor-success?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-Open_Source-orange?style=for-the-badge)]()

---

*Stop getting generic, leaky AI code. Get production-grade, leak-free, mathematically sound data science.*

</div>

---

## 🎯 Why This Skill Pack?

Most AI models give you **fast but flawed** data science code. They fit scalers before splitting, use raw accuracy on 99:1 imbalanced datasets, randomly shuffle time series data, and guess at error fixes.

**These skills enforce the rigorous workflows of senior practitioners across any LLM:**

| ❌ Default AI Output | ✅ With This Skill Pack |
|---|---|
| Fits scaler on full data before splitting | Leak-free `Pipeline` + `ColumnTransformer` |
| Uses `accuracy` on imbalanced data | Chooses metrics by problem: PR-AUC, MASE, F1 |
| Random train/test split on time series | Chronological split with walk-forward validation |
| Clamps negative R² to zero | Reports honest metrics with limitations |
| Generic "try Random Forest" suggestions | Baseline → justified comparison → trade-offs |
| Spaghetti SQL with `SELECT *` | Optimized CTEs, indexing, parameterized queries |
| `plt.plot(data)` with no labels | Publication-quality visuals with insight-driven titles |
| "Just fine-tune BERT" for any text task | TF-IDF baseline first, transformer only when justified |
| Guesses at traceback fixes | Systematic root-cause diagnosis before any code change |
| P-hacking with uncorrected multiple tests | Proper hypothesis testing with effect sizes & power analysis |

---

## 📦 All 10 Skills at a Glance

### 🔬 Core Data Science & Analytics

| # | Skill | What It Does |
|---|---|---|
| 1 | **[`engineering-copilot`](skills/engineering-copilot/SKILL.md)** | 🎯 **Master coordinator** — routes your task to the right workflow, enforces production code standards, data-science correctness rules, and baseline-first thinking across all skills |
| 2 | **[`dataset-intelligence`](skills/dataset-intelligence/SKILL.md)** | 📊 **Data profiling & quality** — missingness analysis, dtype validation, outlier flagging, leakage detection, and actionable cleaning recommendations with reproducible Pandas code |
| 3 | **[`statistical-analysis`](skills/statistical-analysis/SKILL.md)** | 📐 **Hypothesis testing & experimentation** — t-tests, ANOVA, chi-squared, A/B testing with power analysis, causal inference, Bayesian analysis, and proper multiple-comparison corrections |
| 4 | **[`data-visualization-storytelling`](skills/data-visualization-storytelling/SKILL.md)** | 📈 **Charts & communication** — chart selection guide, design principles, matplotlib/seaborn/plotly code, dashboard design, and data storytelling structure for stakeholder presentations |

### 🤖 Machine Learning & AI

| # | Skill | What It Does |
|---|---|---|
| 5 | **[`ml-workflow-engineering`](skills/ml-workflow-engineering/SKILL.md)** | ⚙️ **End-to-end ML pipelines** — problem framing, leak-free preprocessing with `Pipeline`/`ColumnTransformer`, validation strategy selection (stratified, group-aware, chronological), model comparison |
| 6 | **[`time-series-forecasting`](skills/time-series-forecasting/SKILL.md)** | 📉 **Temporal data & forecasting** — seasonal decomposition, stationarity testing, ARIMA/Prophet/ML approaches, walk-forward validation, anomaly detection, and multi-step forecasting |
| 7 | **[`nlp-text-analytics`](skills/nlp-text-analytics/SKILL.md)** | 💬 **Text & language processing** — text preprocessing, TF-IDF/embeddings/transformers, sentiment analysis, NER, topic modeling, RAG pipelines, and LLM fine-tuning workflows |
| 8 | **[`model-evaluation-deployment`](skills/model-evaluation-deployment/SKILL.md)** | 🚀 **Metrics & production** — comprehensive evaluation (confusion matrices, PR-AUC, MASE), FastAPI serving, Docker packaging, CI/CD, cloud deployment, and production-readiness checklists |

### 🔧 Engineering, SQL & Debugging

| # | Skill | What It Does |
|---|---|---|
| 9 | **[`root-cause-debugging`](skills/root-cause-debugging/SKILL.md)** | 🐛 **Systematic debugging** — traceback analysis, shape/dtype mismatch diagnosis, dependency issues, minimal verified fixes, and regression-guarding verification steps |
| 10 | **[`sql-data-engineering`](skills/sql-data-engineering/SKILL.md)** | 🗄️ **SQL & data pipelines** — query optimization, window functions, schema design, ETL/ELT patterns, dbt workflows, BigQuery/Snowflake/PostgreSQL best practices |

---

## 🛠️ How to Use with Any AI Platform

Because every skill is written in clean, universal Markdown, you can drop them into **any** AI platform:

---

### 🟢 1. Using in ChatGPT (OpenAI)

You can use these skills in ChatGPT in three ways:

#### Option A: Build a Custom GPT (Best Experience)
1. Go to [chatgpt.com/gpts/editor](https://chatgpt.com/gpts/editor) (or click **Explore GPTs** → **+ Create**).
2. Under the **Configure** tab:
   - **Name:** `DS/ML Engineering Copilot`
   - **Description:** `Expert Data Science & Machine Learning engineering partner for leak-free pipelines, rigorous analysis, debugging, and deployment.`
   - **Instructions:** Copy & paste the prompt from [WEB_SKILLS.md (Option A)](WEB_SKILLS.md) or the individual [engineering-copilot/SKILL.md](skills/engineering-copilot/SKILL.md).
   - **Capabilities:** Enable **Code Interpreter & Data Analysis** and **Web Search**.
3. (Optional) Upload the `skills/` markdown files to the **Knowledge** section of the GPT.
4. Click **Create** / **Publish**!

#### Option B: ChatGPT Custom Instructions
If you want these rules applied to *every* standard chat session:
1. Click your profile avatar → **Custom instructions** (or **Settings** → **Personalization**).
2. In the box *"How would you like ChatGPT to respond?"*, paste the core rules from [engineering-copilot/SKILL.md](skills/engineering-copilot/SKILL.md#operating-principles).

#### Option C: ChatGPT Projects / Direct Chat
- Paste the contents of any specific `SKILL.md` (e.g., `time-series-forecasting` or `root-cause-debugging`) directly into the start of your chat when tackling a specific task.

---

### 🔵 2. Using in Google Gemini

#### Gemini Web (gemini.google.com)
1. Navigate to **[gemini.google.com/customize/skills](https://gemini.google.com/customize/skills)** (or Gems).
2. Click **`+ Create`**.
3. Use the ready-to-copy prompts in [WEB_SKILLS.md](WEB_SKILLS.md) to create an All-in-One Copilot or separate modular skills.

#### Local Gemini / Antigravity IDE
Install globally across all local projects with a single command:
```bash
mkdir -p ~/.gemini/config/skills
cp -r skills/* ~/.gemini/config/skills/
```

---

### 🟣 3. Using in Claude (Anthropic)

- **Claude Projects:** Create a project (e.g., *"Data Science Studio"*).
  - Add the All-in-One instructions to the **Project Instructions**.
  - Add individual `SKILL.md` files into the **Project Knowledge** base.
- **Claude Web:** Paste any specific `SKILL.md` into your prompt when starting an analysis.

---

### 💻 4. Using in Cursor, Windsurf & AI Coding IDEs

- Copy the skills into your project repository under `.agents/skills/` or `.cursorrules`:
```bash
mkdir -p .agents/skills
cp -r path/to/ds-ml-skills/skills/* .agents/skills/
```
Your local AI agent will automatically detect the skills and activate them during development.

---

## 💡 Prompt Examples

Once loaded into your AI of choice, just prompt naturally:

| What You Ask | Skill That Kicks In |
|---|---|
| *"Profile this customer churn CSV and check for quality issues"* | `dataset-intelligence` |
| *"Is the conversion difference between variant A and B statistically significant?"* | `statistical-analysis` |
| *"Create an executive-level dashboard showing regional revenue trends"* | `data-visualization-storytelling` |
| *"Design a baseline and leak-free pipeline for this tabular classification task"* | `ml-workflow-engineering` |
| *"Forecast the next 12 months of demand from this monthly sales dataset"* | `time-series-forecasting` |
| *"Classify these support tickets into categories with confidence scores"* | `nlp-text-analytics` |
| *"Package this model into a FastAPI service with Docker and health checks"* | `model-evaluation-deployment` |
| *"Debug this PyTorch shape mismatch error in my custom attention layer"* | `root-cause-debugging` |
| *"Optimize this slow analytical query with window functions and indexing"* | `sql-data-engineering` |

---

## 🏗️ Repository Structure

```
ds-ml-skills/
├── README.md                                    # Comprehensive guide & cross-platform setup
├── WEB_SKILLS.md                                # Copy-paste prompts for web UIs (ChatGPT / Gemini / Claude)
├── plugin.json                                  # Agent plugin manifest
└── skills/
    ├── engineering-copilot/SKILL.md              # 🎯 Master coordinator & correctness rules
    ├── dataset-intelligence/SKILL.md             # 📊 Data profiling & EDA reconnaissance
    ├── statistical-analysis/SKILL.md             # 📐 Hypothesis testing, A/B testing & causal inference
    ├── data-visualization-storytelling/SKILL.md  # 📈 Charts, styling & stakeholder storytelling
    ├── ml-workflow-engineering/SKILL.md           # ⚙️ Leak-free pipelines & validation splits
    ├── time-series-forecasting/SKILL.md          # 📉 Chronological splits, decomposition & models
    ├── nlp-text-analytics/SKILL.md               # 💬 NLP, embeddings, transformers & RAG
    ├── model-evaluation-deployment/SKILL.md      # 🚀 Metrics, APIs, Docker & production checklists
    ├── root-cause-debugging/SKILL.md             # 🐛 Systematic traceback diagnosis & minimal fixes
    └── sql-data-engineering/SKILL.md             # 🗄️ SQL optimization, schemas & ELT pipelines
```

---

## 🎓 Who Is This For?

| Role | Most Valuable Skills |
|---|---|
| **Data Analyst** | `dataset-intelligence`, `statistical-analysis`, `data-visualization-storytelling`, `sql-data-engineering` |
| **Data Scientist** | Full toolkit — end-to-end data exploration, validation design, modeling, and evaluation |
| **ML Engineer** | `ml-workflow-engineering`, `model-evaluation-deployment`, `root-cause-debugging`, `nlp-text-analytics` |
| **Analytics Engineer** | `sql-data-engineering`, `dataset-intelligence`, `data-visualization-storytelling` |
| **Students & Beginners** | All skills — learns the *right* way to do data science without cutting dangerous corners |

---

## 🧬 Core Engineering Tenets

1. **Evidence First** — Inspect shapes, schemas, and tracebacks before claiming an answer or writing mutations.
2. **Baselines First** — Test Dummy/Naive models before jumping to XGBoost or Deep Learning.
3. **Never Fake Cleanliness** — Negative $R^2$ is valid; outliers are investigation flags, not automatic drops.
4. **Leak-Free by Construction** — Preprocessing lives inside pipelines fitted strictly on training splits.
5. **Production Mindset** — Modular functions, typed inputs, reproducible seeds, and explicit failure modes.

---

## 🤝 Contributing

Have ideas for new skills (e.g., Computer Vision, Recommendation Systems, Graph Analytics)?
1. Fork the repo.
2. Add your skill folder under `skills/<skill-name>/SKILL.md`.
3. Submit a PR!

---

## 📄 License

Open source under MIT License. Free to use, adapt, and share across any platform.
