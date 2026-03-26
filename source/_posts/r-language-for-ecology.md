---
title: R Language for Ecology — R语言生态学使用手册
date: 2025-04-27 10:00:00
categories:
  - Tools-Resources
tags:
  - R
  - Ecology
  - Data Analysis
  - Programming
---

# R Language for Ecology — R语言生态学使用手册

> R语言在生态学数据分析中的使用方法与技巧，课程：Introduction to Scientific Computing & Statistical Methods

## 适用领域
- 生态学数据分析与可视化
- 物种分布建模
- 系统发育分析
- 种群动态建模

## 核心技能点

### R 基础
- 数据类型与向量操作
- R包安装与加载（install.packages / library）
- 函数式编程与管道操作（`%>%`）

### 数据整理 (Tidyverse)
- `read_csv()` — 数据导入
- `dplyr`：filter/select/mutate/group_by/summarise
- `tidyr`：pivot_longer/pivot_wider
- `left_join()` — 数据连接

### 数据可视化 (ggplot2)
- 图形语法：`ggplot() + aes() + geom_*()`
- 常用图层：geom_point/geom_line/geom_bar/geom_boxplot
- 美化：labs/theme/scale_color_brewer

### 统计建模
- 线性模型：`lm()`
- 广义线性模型：`glm()`
- 混合模型：`lme4::glmer()`

### R Markdown
- 可重复研究报告
- 代码块与输出整合

## 实战代码笔记

### 构建基因树 — Phylogenies in R
```r
library(ape)
library(phytools)
library(tidyverse)

# 读取树文件
tree <- read.tree("phylogenetic_tree.nwk")

# 计算系统发育信号
physignal <- phylosig(tree, trait_data, method="K")

# 绘制系统发育树
plotTree(tree, fsize=0.8, ftype="i")
```

### 统计分析示例
```r
# 广义线性混合模型
library(lme4)
model <- glmer(cbind(success, failure) ~ treatment + (1|block),
               family = binomial, data = mydata)
summary(model)
```

## 参考资源
- [R for Data Science](https://r4ds.had.co.nz/)
- [Ecological Models with R](https://github.com/)
- 课程：Introduction to Scientific Computing & Statistical Methods
