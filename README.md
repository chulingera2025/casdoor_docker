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

## Troubleshooting

### Local file storage permission denied

If you configured Casdoor Storage to use the **Local** provider, file uploads may fail with an error like:

```
Casdoor fails to create folder: "/files/resource/built-in/admin" for local file system storage provider: mkdir /files/resource: permission denied. Make sure Casdoor process has correct permission to create/access it, or you can create it manually in advance.
```

This happens because the container runs as UID 1000 and cannot write to the `files/` directory created by Docker.

**Solution:** Change ownership and permissions on the `files/` directory (auto-created next to `docker-compose.yml`):

```bash
sudo chown -R 1000:1000 files
sudo chmod -R 755 files
```

After this, restart the stack:

```bash
docker compose down && docker compose up -d
```

## Links

- Official Casdoor repository: https://github.com/casdoor/casdoor

## License

This project is licensed under the MIT License.
