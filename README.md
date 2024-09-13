# sync_dify_image

## 功能

- 从 Docker Hub 拉取镜像
- 将镜像推送到阿里云 ACR
- 支持通过 Docker Compose 文件自动解析和同步镜像

## 配置 GitHub Secrets

在 GitHub 仓库设置中，添加以下 secrets：

- `ACR_USERNAME`: 阿里云 ACR 用户名
- `ACR_PASSWORD`: 阿里云 ACR 密码
- `ACR_REGISTRY`: 阿里云 ACR 注册表地址（例如：`your-registry-id.cn-hangzhou.aliyuncs.com`）

## 工作流

GitHub Actions 工作流定义文件位于 `.github/workflows/sync-images.yml`。工作流的主要步骤如下：

1. **从 `dify` 仓库读取镜像**：工作流会检查 `langgenius/dify` 仓库中的代码，并读取 `docker/docker-compose.yaml` 文件中的镜像定义。
2. **解析 Docker Compose 文件**：使用 `yq` 工具从 `docker-compose.yaml` 文件中提取镜像名称。
3. **登录到阿里云 ACR**：使用配置的 GitHub Secrets 登录到阿里云 ACR。
4. **拉取、标记和推送镜像**：拉取 Docker Hub 上的镜像，标记并推送到阿里云 ACR。

## 使用

每当你将代码推送到 `main` 分支时，GitHub Actions 将自动执行上述工作流，确保镜像在 Docker Hub 和阿里云 ACR 之间保持同步。
