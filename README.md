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
修改dify-version.txt,当你将代码推送到 `main` 分支时，GitHub Actions 将自动执行上述工作流，确保镜像在 Docker Hub 和阿里云 ACR 之间保持同步。


| 源镜像                                          | 替换后镜像                                                     |
|-------------------------------------------------|----------------------------------------------------------------|
| langgenius/dify-api:0.8.2                       | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/dify-api:0.8.2     |
| langgenius/dify-web:0.8.2                       | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/dify-web:0.8.2     |
| postgres:15-alpine                              | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/postgres:15-alpine  |
| redis:6-alpine                                  | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/redis:6-alpine      |
| langgenius/dify-sandbox:0.2.7                   | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/dify-sandbox:0.2.7 |
| ubuntu/squid:latest                             | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/squid:latest |
| certbot/certbot                                 | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/certbot:latest |
| nginx:latest                                    | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/nginx:latest        |
| semitechnologies/weaviate:1.19.0                | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/weaviate:1.19.0 |
| langgenius/qdrant:v1.7.3                        | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/qdrant:v1.7.3      |
| pgvector/pgvector:pg16                          | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/pgvector:pg16 |
| tensorchord/pgvecto-rs:pg16-v0.3.0              | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/pgvecto-rs:pg16-v0.3.0 |
| ghcr.io/chroma-core/chroma:0.5.1                | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/chroma:0.5.1 |
| container-registry.oracle.com/database/free:latest | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/free:latest |
| quay.io/coreos/etcd:v3.5.5                      | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/etcd:v3.5.5 |
| minio/minio:RELEASE.2023-03-20T20-16-18Z        | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/minio:RELEASE.2023-03-20T20-16-18Z |
| milvusdb/milvus:v2.3.1                          | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/milvus:v2.3.1 |
| opensearchproject/opensearch:latest             | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/opensearch:latest |
| opensearchproject/opensearch-dashboards:latest  | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/opensearch-dashboards:latest |
| myscale/myscaledb:1.6.4                         | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/myscaledb:1.6.4 |
| docker.elastic.co/elasticsearch/elasticsearch:8.14.3 | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/elasticsearch:8.14.3 |
| docker.elastic.co/kibana/kibana:8.14.3          | registry.cn-hangzhou.aliyuncs.com/kenwood-ai/kibana:8.14.3 |
