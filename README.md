# TokenDanceLab · org 元仓

TokenDanceLab GitHub 组织的社区文件元仓：profile 首页、issue/PR 模板、行为规范与安全策略。

## 内容

- `profile/README.md` — 组织首页
- `ISSUE_TEMPLATE/` · `PULL_REQUEST_TEMPLATE.md` — issue/PR 模板
- `CODE_OF_CONDUCT.md` · `CONTRIBUTING.md` · `SECURITY.md` — 社区与安全规范

## CI/CD 策略

**不统一 CI，各仓自治**（决策记录：issue #2）。各仓库在自身 `.github/workflows/` 维护适合自己的 workflow；本仓不提供 callable 或模板。

仓库 CI 强度参考分类（指导，非强制模板）：

| 分类 | 定义 | CI 强度 |
|------|------|---------|
| **A** 自有产品 | 无上游 merge 压力的产品 | 完整（lint → test → build → vulncheck → 镜像） |
| **B** Fork | 跟上游、有补丁面 | 轻量 overlay + upstream-sync |
| **C** 配置/部署 | deploy/nginx 清单 | 校验 |
| **D** 已退役 | 生产关停 | 最低 |
| **E** 文档/展示 | docs/design | path-filter 轻量 |

## 安全红线

- **不要在 workflow 中硬编码 IP、host、secret。** 敏感信息通过 GitHub Secrets 注入。
- L3 CD 推送 GHCR ≠ 自动部署。生产部署走独立 SOP。
- fork 仓库尽量不改上游 workflow 文件，TD 自有 CI 用 `td-*.yml` 前缀。

---

> 完整 CI/CD 策略见内部文档。本 README 为公开摘要，不包含运维细节。
