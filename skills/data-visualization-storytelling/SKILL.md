---
name: data-visualization-storytelling
description: Use when the user needs to create charts, dashboards, data presentations, or communicate analytical findings to stakeholders. Covers matplotlib, seaborn, plotly, altair, and dashboard frameworks.
---

# Data Visualization & Storytelling

Create clear, honest, and compelling visualizations. A chart should answer a question, not just display data.

## 1. Understand the audience and message

Before writing any plotting code, clarify:

- **Who** is the audience? Technical team, business stakeholders, executives, or public?
- **What** is the one key insight or question this visual should answer?
- **What decision** does this support?

Choose complexity accordingly: exploratory plots for yourself can be rough; stakeholder-facing visuals must be polished and self-explanatory.

## 2. Choose the right chart type

| Question | Recommended Chart |
|---|---|
| Distribution of a single numeric variable | Histogram, KDE plot, box plot, violin plot |
| Comparing categories | Bar chart (horizontal for many categories), grouped/stacked bar |
| Relationship between two numeric variables | Scatter plot, hexbin (large N), regression plot |
| Trend over time | Line chart with clear x-axis time labels |
| Part-to-whole composition | Stacked bar, treemap, waffle chart. Avoid pie charts unless ≤5 segments |
| Ranking | Horizontal bar chart sorted by value |
| Correlation matrix | Heatmap with annotated values and masked upper triangle |
| Geographic data | Choropleth map, scatter on map |
| Multiple distributions to compare | Overlapping KDE, ridge plot, faceted histograms |
| Categorical × Numeric | Box plot, violin plot, strip/swarm plot |

Never use 3D charts for 2D data. Avoid dual y-axes unless absolutely necessary and clearly labeled.

## 3. Design principles

- **Title**: every chart must have a clear, descriptive title that states the insight, not just the variable names. Example: "Revenue grew 23% YoY driven by APAC expansion" instead of "Revenue by Region".
- **Labels**: axis labels with units, readable font sizes, no overlapping text. Rotate or abbreviate long labels.
- **Color**: use colorblind-friendly palettes (e.g., `tab10`, `colorblind`, viridis family). Use color intentionally to highlight, not to decorate. Use a single accent color to draw attention to the key data point.
- **Legend**: place near the data it describes. Remove if unnecessary (direct labeling is often better).
- **Grid**: light gridlines to aid reading; remove chartjunk (unnecessary borders, background fills, 3D effects).
- **Aspect ratio**: use wide ratios (16:9) for time series and trends; square or tall ratios for comparisons.
- **Annotation**: annotate key data points, thresholds, or events directly on the chart.
- **Scale**: start numeric axes at zero for bar charts. Use log scale when data spans orders of magnitude and explain it.

## 4. Library selection

- **matplotlib**: full control, publication-quality static plots. Use `plt.subplots()` pattern consistently.
- **seaborn**: statistical visualizations with sensible defaults. Use `sns.set_theme()` for consistent styling.
- **plotly**: interactive charts for dashboards, notebooks, and web apps. Use `plotly.express` for speed, `plotly.graph_objects` for customization.
- **altair**: declarative grammar-of-graphics approach. Best for exploratory visualization and faceted views.

When providing code, always include: imports, figure sizing, titles, axis labels, and `plt.tight_layout()` or equivalent. Save with appropriate DPI for the intended medium (150+ for reports, 300 for print).

## 5. Dashboard design

When building analytical dashboards (Streamlit, Dash, Panel, Gradio):

- Lead with the most important KPI or metric at the top.
- Use filters and interactivity to let users drill down without cluttering the main view.
- Group related metrics together. Use consistent color coding across all charts.
- Include date range selectors and comparison periods (MoM, YoY).
- Add data freshness timestamps and source attribution.
- Keep the dashboard focused: 5–8 charts maximum per view.

## 6. Data storytelling structure

For presentations and reports, structure the narrative as:

1. **Context**: what question are we answering and why does it matter?
2. **Key finding**: state the answer upfront with a clear visual.
3. **Supporting evidence**: 2–3 additional charts that reinforce or add nuance.
4. **So what?**: implications, recommended actions, and next steps.
5. **Caveats**: data limitations, assumptions, and confidence levels.

## 7. Honesty rules

- Never truncate axes to exaggerate differences without explicit disclosure.
- Never cherry-pick date ranges to support a narrative.
- Show uncertainty: confidence intervals, error bars, or prediction bands when available.
- Disclose sample sizes, filters applied, and excluded data points.
- Label estimated or projected values distinctly from actual data.
