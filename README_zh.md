# Casdoor Docker 生产部署

这是一个基于 Docker Compose 的 Casdoor 生产环境部署项目，集成了 Casdoor、MySQL 和 Redis，用于快速完成自托管部署。

[English README](./README.md)

## 快速开始

```bash
cd casdoor_redis
cp .env.example .env
```

修改 `.env` 中的生产环境配置，重点是：

```env
CASDOOR_ORIGIN=https://auth.example.com
MYSQL_ROOT_PASSWORD=your_strong_password
MYSQL_DATABASE=casdoor
```

然后启动：

```bash
docker compose up -d
```

启动完成后，通过你配置的域名或服务器 `8000` 端口访问 Casdoor。

## 相关链接

- Casdoor 官方仓库: https://github.com/casdoor/casdoor
- 也欢迎给我维护的 Casnode 点个 Star: https://github.com/chulingera2025/casnode

## 许可证

本项目采用 MIT License。
