# FIFA 世界杯赛程优化项目

这个项目围绕 FIFA 世界杯小组赛赛程设计，搭建了一个三阶段优化模型框架。项目目标是在 48 支球队的新赛制下，同时考虑小组实力均衡、比赛热度分布和球场容量分配。

## 项目概览

本项目把大型体育赛事赛程安排视为一个 prescriptive analytics 问题。模型使用 FIFA 排名积分、洲际足联限制、观众需求代理变量、比赛热度指标和球场容量数据，辅助制定更合理的赛程安排方案。

整个优化流程分为三个阶段：

1. 小组均衡分配
2. 基于比赛热度的小组字母分配
3. 基于 row-set 热度和球场容量的场馆分配

## 业务问题

大型体育赛事的赛程安排通常需要同时满足多个目标：

- 保证各小组整体实力相对均衡
- 遵守抽签规则，例如档位结构和洲际足联限制
- 将高热度比赛更合理地分布到赛程中
- 将更受关注的比赛组合分配到容量更大的球场

这个项目展示了如何用数学优化模型把这些复杂约束和目标转化为可执行的分析流程。

## 方法设计

### 模型一：小组均衡分配

第一个模型将 48 支球队分配到 12 个小组，每组 4 支球队。模型使用 FIFA ranking points 作为球队实力的代理变量。

目标函数：

- 最大化所有小组中的最低小组总实力

主要约束：

- 每支球队只能被分到一个小组
- 每个小组必须有 4 支球队
- 每个小组必须包含每个档位的一支球队
- 满足洲际足联相关限制

该模型使用 Pyomo 建模，并使用 GLPK 求解。

### 模型二：小组字母分配

第二个模型将模型一得到的小组分配到 A 到 L 的小组字母。比赛热度根据每支球队的 spectator index 计算。

目标函数：

- 平衡不同 row-set 的比赛热度

该模型使用 Google OR-Tools CP-SAT 实现。

### 模型三：球场分配

第三个模型根据 row-set 热度和球场容量，将 row-set 分配到 16 个世界杯球场。

目标函数：

- 最大化整体 spectator exposure

该模型使用 Pyomo 建模，并使用 GLPK 求解。

## 数据说明

项目使用整理后的 Excel 工作簿，主要包含：

- FIFA 排名积分和球队所属洲际足联
- 2026 FIFA 世界杯球场容量数据
- 历史上座率和观众需求代理变量
- 小组赛赛程结构
- 中间模型结果

主要数据文件：

```text
data/world_cup_scheduling_data.xlsx
```

## 关键结果

- 搭建了适用于 48 支球队、12 个小组赛制的三阶段优化流程。
- 生成了均衡小组分配方案，最低小组总实力为 6,341.67 ranking points。
- 将小组分配到 A-L 字母，以平衡 16 个 row-set 的比赛热度。
- 将 row-set 分配到 16 个球场，得到约 5.34 million 的最优 spectator exposure 目标值。

## 文件结构

```text
world-cup-scheduling-optimisation/
├── README.md
├── README.zh-CN.md
├── requirements.txt
├── data/
│   └── world_cup_scheduling_data.xlsx
├── docs/
│   └── project_summary.md
└── notebooks/
    └── world_cup_scheduling_optimisation.ipynb
```

## 使用工具

- Python
- pandas
- Pyomo
- Google OR-Tools CP-SAT
- GLPK
- Excel

## 如何运行

安装 Python 依赖：

```bash
pip install -r requirements.txt
```

如果本地还没有 GLPK，需要单独安装 GLPK 求解器。

然后打开并运行：

```text
notebooks/world_cup_scheduling_optimisation.ipynb
```

## 简历项目总结

这个项目展示了如何将优化建模用于大型赛事排程和资源分配问题。项目结合了数据整理、数学规划、约束建模和业务解释，适合放在 Business Analytics、Data Analyst、Operations Analyst 或 Optimisation Analytics 相关岗位的作品集中。
