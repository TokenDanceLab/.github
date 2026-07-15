# TokenDanceLab · 组织级 CI/CD 模板

可复用 workflow 与模板，供 TokenDanceLab 下各仓库接入标准化 CI/CD。

## 快速开始 — 新仓库

```bash
mkdir -p .github/workflows
cp workflow-templates/ci-go-service.yml .github/workflows/ci.yml
```

修改 `ci.yml` 顶部 `with:` 参数（Go 版本、工作目录等），push 即可。

## 可用模板

| 模板 | 用途 | 调用方式 |
|------|------|----------|
| `ci-go-service.yml` | Go 服务：lint → test → build → vulncheck | 复制到仓库 |
| `cd-ghcr-image.yml` | Docker 镜像构建 + GHCR 推送 | 复制到仓库 |
| `cd-pr-check.yml` | PR 质量门禁 | 复制到仓库 |

三个模板也支持 `workflow_call`，已有仓库可直接引用：

```yaml
jobs:
  ci:
    uses: TokenDanceLab/.github/.github/workflows/ci-go-service.yml@main
    with:
      go_version: "1.25"
```

## 仓库 CI 分类

新仓库按类型选择 CI 强度：

| 分类 | 定义 | 模板 | CI 强度 |
|------|------|------|---------|
| **A** 自有产品 | 无上游 merge 压力的产品 | `ci-go-service` + `cd-ghcr-image` | 完整 |
| **B** Fork | 跟上游、有补丁面 | Overlay CI + `upstream-sync.yml` | 轻量 |
| **C** 配置/部署 | deploy/nginx 清单 | — | 校验 |
| **D** 已退役 | 生产关停 | — | 最低 |
| **E** 文档/展示 | docs/design | path-filter | 轻量 |

## 安全红线

- **不要在 workflow 中硬编码 IP、host、secret。** 敏感信息通过 GitHub Secrets 注入。
- L3 CD 推送 GHCR ≠ 自动部署。生产部署走独立 SOP。
- fork 仓库尽量不改上游 workflow 文件，TD 自有 CI 用 `td-*.yml` 前缀。

---

> 完整 CI/CD 策略见内部文档。本 README 为公开摘要，不包含运维细节。
