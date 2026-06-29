# Casdoor Docker 生产部署

这是一个基于 Docker Compose 的 Casdoor 生产环境部署项目，集成了 Casdoor、MySQL 和 Redis，用于快速完成自托管部署。

[English README](./README.md)

## 快速开始

```bash
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

## Nginx 反向代理（可选）

项目提供了 `casdoor.conf`，包含 HTTP→HTTPS 重定向和 HTTPS 反代，仅使用 HTTP/1.1。

使用方法：

1. 编辑 `casdoor.conf`，替换 `server_name` 为你的域名，填入真实的 SSL 证书路径（搜索 `← 替换为真实路径`）
2. 部署并启用：

```bash
sudo cp casdoor.conf /etc/nginx/sites-available/casdoor.conf
sudo ln -s /etc/nginx/sites-available/casdoor.conf /etc/nginx/sites-enabled/casdoor.conf
sudo nginx -t && sudo systemctl reload nginx
```

## 相关链接

- Casdoor 官方仓库: https://github.com/casdoor/casdoor

## 许可证

本项目采用 MIT License。
