# spoke-immich

Spoke module for [Immich](https://immich.app/) self-hosted photo and video management.

## Services

| Service                | Description                | Port | Network |
|------------------------|----------------------------|------|---------|
| immich-server          | Main application server    | 2283 | troxy   |
| immich-machine-learning| ML inference (face/object) | 3003 | troxy   |
| immich-postgres        | PostgreSQL with pgvecto.rs | 5432 | troxy   |
| immich-redis           | Valkey cache & job queue   | 6379 | troxy   |

## Prerequisites

- Spoke hub deployed with `troxy` network
- Traefik available as a hub service
- GPU passthrough (`/dev/dri`) for hardware transcoding
- `immich_db_password` secret created

## Quick Start

```bash
cp .env.example .env
# Edit .env — set data paths
docker compose up -d
```

## Module Environment Variables

| Variable                        | Default                                                           | Description            |
|---------------------------------|-------------------------------------------------------------------|------------------------|
| `IMMICH_VERSION`                | `v2.5.6`                                                         | Immich version tag     |
| `IMMICH_SERVER_IMAGE`           | `ghcr.io/immich-app/immich-server:v2.5.6`                        | Server image           |
| `IMMICH_MACHINE_LEARNING_IMAGE` | `ghcr.io/immich-app/immich-machine-learning:v2.5.6`              | ML image               |
| `IMMICH_POSTGRES_IMAGE`         | `ghcr.io/immich-app/postgres:14-vectorchord0.4.3-pgvectors0.2.0` | Postgres image         |
| `IMMICH_REDIS_IMAGE`            | `docker.io/valkey/valkey:9`                                      | Valkey/Redis image     |
| `IMMICH_SERVER_IP`              | `192.168.35.28`                                                  | Server static IP       |
| `IMMICH_ML_IP`                  | `192.168.35.29`                                                  | ML static IP           |
| `IMMICH_POSTGRES_IP`            | `192.168.35.30`                                                  | Postgres static IP     |
| `IMMICH_REDIS_IP`               | `192.168.35.31`                                                  | Redis static IP        |
| `IMMICH_DB_USER`                | `immich`                                                         | Database username      |
| `IMMICH_DB_NAME`                | `immich`                                                         | Database name          |

## References

- [Immich Documentation](https://immich.app/docs)
- [Immich GitHub](https://github.com/immich-app/immich)
