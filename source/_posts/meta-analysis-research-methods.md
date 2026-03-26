---
title: "Meta-Analysis Research Methods — 元分析研究方法"
date: 2025-04-27 11:00:00
categories:
  - Tools-Resources
tags:
  - Meta-Analysis
  - R
  - Evidence Synthesis
  - Statistics
---

# Meta-Analysis Research Methods — 元分析研究方法

> 元分析是综合多个独立研究结果的统计方法，课程：Marcoecology and Global Change

## 适用领域
- 生态学效应量综合
- 保护干预效果评估
- 系统综述与证据合成

## 核心工具
- **metafor** — R语言元分析核心包
- **orchaRd** — 效应量可视化
- **ggplot2** — 图表绑定
- **patchwork** — 多图拼接

## 核心概念

### 效应量 (Effect Size)
- 均值差 (SMD) — 连续变量
- 相关系数 (r) — 关联强度
- 风险比 (OR) — 二分类数据
- 响应比 (RR) — 生态学常用

### 异质性检验
- **Q检验** — 研究间是否存在显著异质性
- **I²** — 异质性比例（>75%为高异质性）
- **τ²** — 研究间方差

### 模型选择
- **固定效应模型 (FE)** — 假设所有研究估计同一真实效应
- **随机效应模型 (RE)** — 允许效应量在研究间变化（生态学常用）
- **混合效应模型** — 加入调节变量

## 实战代码笔记

### 基本元分析流程
```r
library(metafor)
library(orchaRd)
library(tidyverse)

# 1. 读取数据
dat <- read.csv("Data_Extraction.csv")

# 2. 计算效应量
dat <- escalc(measure = "ROM",
              m1i = mean_treatment, sd1i = sd_treatment, n1i = n_treatment,
              m2i = mean_control, sd2i = sd_control, n2i = n_control,
              data = dat)

# 3. 随机效应模型
res <- rma(yi, vi, data = dat, method = "REML")
summary(res)

# 4. 森林图
forest(res, slab = dat$study_id, xlab = "Response Ratio")
orchard_plot(res, mod = "grouping_variable", data = dat)

# 5. 漏斗图 (发表偏倚)
funnel(res, xlab = "Effect Size")
regtest(res)  # Egger's test
```

### 亚组分析与元回归
```r
# 亚组分析
res_subgroup <- rma(yi, vi, mods = ~ treatment_type, data = dat, method = "REML")
anova(res_subgroup)

# 元回归
res_metareg <- rma(yi, vi, mods = ~ temperature, data = dat, method = "REML")
```
