# Casdoor Docker Deployment

This project provides a Docker Compose based production deployment for Casdoor, bundled with Casdoor, MySQL, and Redis for quick self-hosting.

[中文文档](./README_zh.md)

## Quick Start

```bash
cp .env.example .env
```

Update `.env` with your production settings, especially:

```env
CASDOOR_ORIGIN=https://auth.example.com
MYSQL_ROOT_PASSWORD=your_strong_password
MYSQL_DATABASE=casdoor
```
> Generate a strong MySQL password: `openssl rand -hex 32`

Then start the stack:

```bash
docker compose up -d
```

After startup, access Casdoor from your configured domain or from port `8000` on the server.

> `runmode` in `conf/app.conf` accepts `dev` / `prod` / `test`. `docker-compose.yml` already overrides it to `prod` via environment variable.

## Nginx Reverse Proxy (optional)

A `casdoor.conf` is included with HTTP→HTTPS redirect and HTTPS reverse proxy, using HTTP/1.1 only.

Usage:

1. Edit `casdoor.conf` — replace `server_name` with your domain, fill in real SSL certificate paths
2. Deploy:

```bash
sudo cp casdoor.conf /etc/nginx/sites-available/casdoor.conf
sudo ln -s /etc/nginx/sites-available/casdoor.conf /etc/nginx/sites-enabled/casdoor.conf
sudo nginx -t && sudo systemctl reload nginx
```

## Links

- Official Casdoor repository: https://github.com/casdoor/casdoor

## License

This project is licensed under the MIT License.
