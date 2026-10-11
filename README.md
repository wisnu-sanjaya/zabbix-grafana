# Zabbix 7.0 + Grafana (Docker Compose)

Semua data di ./data (tidak masuk git). Zabbix :8081, Grafana :3001.

## Deploy
    git clone git@github.com:wisnu-sanjaya/zabbix-grafana.git /opt/docker/zabbix
    cd /opt/docker/zabbix
    cp .env.example .env        # isi ZABBIX_DB_PASSWORD & GRAFANA_ADMIN_PASSWORD
    mkdir -p data/{postgres,backups,grafana} && chown -R 472:0 data/grafana
    docker network create zabbix-network
    docker compose up -d
    # Zabbix: buat user grafana + group Grafana-RO (Read) + API token
    # isi ZABBIX_API_TOKEN di .env, lalu:
    docker compose up -d --force-recreate grafana

## Restore DB
    gunzip -c backup.sql.gz | docker compose exec -T postgres psql -U zabbixdbuser -d zabbixdb
