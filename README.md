# Casdoor Docker Deployment

This project provides a Docker Compose based production deployment for Casdoor, bundled with Casdoor, MySQL, and Redis for quick self-hosting.

[中文文档](./README_zh.md)

## Quick Start

```bash
cd casdoor_redis
cp .env.example .env
```

Update `.env` with your production settings, especially:

```env
CASDOOR_ORIGIN=https://auth.example.com
MYSQL_ROOT_PASSWORD=your_strong_password
MYSQL_DATABASE=casdoor
```

Then start the stack:

```bash
docker compose up -d
```

After startup, access Casdoor from your configured domain or from port `8000` on the server.

## Links

- Official Casdoor repository: https://github.com/casdoor/casdoor
- Also please star my Casnode project: https://github.com/chulingera2025/casnode

## License

This project is licensed under the MIT License.
