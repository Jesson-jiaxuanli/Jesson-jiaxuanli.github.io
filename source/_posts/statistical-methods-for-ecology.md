---
title: "Statistical Methods for Ecology — 生态学统计方法"
date: 2025-08-12 11:00:00
categories:
  - Tools-Resources
tags:
  - Statistics
  - R
  - Modeling
  - GLM
  - Bayesian
---

# Statistical Methods for Ecology — 生态学统计方法

> 生态学研究中的核心统计方法，从基础概率到高级建模。课程：Statistical Methods

## 适用领域
- 种群动态建模
- 物种分布预测
- 实验数据分析
- 环境因子效应评估

## 核心框架

### 概率基础
- 随机变量与概率密度函数 (PDF)
- 累积分布函数 (CDF)
- 期望与方差
- 核心分布：正态、二项、泊松、负二项

### 推断统计
- 总体参数 vs 样本统计量
- 无偏估计
- 假设检验（零假设, p-value）
- 置信区间

### 模型体系

| 模型类型 | 用途 | R函数 |
|---------|------|-------|
| 线性回归 (LM) | 连续响应 | `lm()` |
| 广义线性模型 (GLM) | 非正态响应 | `glm()` |
| 广义线性混合模型 (GLMM) | 分层/重复数据 | `lme4::glmer()` |
| 贝叶斯模型 | 后验概率分布 | `brms::brm()` |

### 频率派 vs 贝叶斯派

| 对比维度 | 频率派 | 贝叶斯派 |
|---------|--------|---------|
| 核心概念 | 最大似然估计 | 后验概率分布 |
| 先验信息 | 不纳入 | 明确纳入 |
| R包 | lm/glm/lme4 | brms/INLA |
| 结果解读 | p-value + CI | 后验分布 + HDI |

## 实战代码笔记

### 线性回归
```r
model_lm <- lm(body_mass ~ body_length + sex, data = birds)
summary(model_lm)
par(mfrow=c(2,2)); plot(model_lm)
```

### 广义线性模型
```r
model_glm <- glm(survival ~ temperature + habitat,
                 family = binomial(link = "logit"), data = experiment)
summary(model_glm)
exp(coef(model_glm))  # Odds Ratio
```

### 混合效应模型
```r
library(lme4)
library(lmerTest)
model_glmm <- glmer(cbind(success, failure) ~ treatment + (1|site),
                    family = binomial, data = data)
summary(model_glmm)
```

### 贝叶斯回归
```r
library(brms)
model_bayes <- brm(response ~ predictor + (1|group),
                   family = gaussian(), data = mydata,
                   chains = 4, iter = 2000)
summary(model_bayes)
plot(model_bayes)
```

## 参考资源
- Zuur et al. (2009) *Mixed Effects Models in R*
- Kéry & Royle (2016) *Applied Hierarchical Models in R*
- McElreath (2020) *Statistical Rethinking*
