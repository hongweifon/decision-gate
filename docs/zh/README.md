> 🇨🇳 简体中文 · [🇺🇸 English](/../../README.md)

# Decision Gate
AI 代理的运行时决策框架。

让代理不仅知道如何执行——更知道何时暂停、改道和求助。

---

## 谁应该使用

长时间运行的编码任务、研究代理、批量数据处理、大规模网页爬取、CI/CD 调试工作流、数据管道、自动化。
**不适于**一次性任务或简单问答。

---

## 架构

用户策略 → 决策策略层 → 强制规则 / 运行时评估 → 健康评估（3 维度）→ 触发引擎
f(阈值, 置信度, 策略) → 路由决策（9 个输出，3 个类别）。

完整架构图请见 [architecture.md](/docs/architecture.md)。

---

## 快速示例

任务：爬取 50 所大学的网站。12 所顺利，38 所使用了自定义 SPA（每个慢 5 倍）。

**没有 Decision Gate：** 代理连续爬取 6+ 小时直至上下文耗尽。
**有了 Decision Gate：** 代理在检查点停下。路由：请求用户。

选项：
- 继续全部 50 所（6–10h）
- 优先完成前 20 所（2h，80% 覆盖）
- 交付已完成的 12 所（0h，24% 覆盖）

---

## 安装

**Codex 参考实现：**
```
codex skills install decision-gate
```

**作为框架使用：**
阅读 [docs/](/docs/)。适用于 Claude、Gemini、LangGraph、AutoGen 或任何代理运行时。

---

## 基准测试

真实环境对比计划在 v0.2 中发布。当前示例仅为定性参考。详见 [benchmarks/](/benchmarks/)。

---

## 为什么有效

- **策略优先于一切**
- **三个健康维度**覆盖执行、需求和决策
- **阈值 × 置信度**抑制误报
- **三类输出**让代理或人类做决定
- **框架适配任何架构**，不局限于某条提示词

---

## 文档

| 文档 | 说明 |
|------|------|
| [philosophy.md](/docs/philosophy.md) | 为什么 |
| [architecture.md](/docs/architecture.md) | 怎么做 |
| [health-model.md](/docs/health-model.md) | 健康维度 |
| [decision-policy.md](/docs/decision-policy.md) | 策略系统 |
| [routing.md](/docs/routing.md) | 输出 |
| [examples.md](/docs/examples.md) | 场景 |
| [faq.md](/docs/faq.md) | 常见问题 |

---

## 链接

- [SKILL.md](/SKILL.md): 参考实现
- [CHANGELOG.md](/CHANGELOG.md)
- [贡献指南](/CONTRIBUTING.md)

---

MIT License
