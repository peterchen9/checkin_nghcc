# Docker 部署規劃

## 原則

本專案必須獨立 Docker 化，與既有「北門行政作業平台」及其他系統分離。現階段只建立本機 skeleton 與部署規劃，不得直接動 production。

## 建議服務

- `web`：前後台應用服務。初期以 Nginx 提供靜態 skeleton，後續可改為前端 build 或後端 API 應用。
- `db`：預留資料庫服務，建議使用 MySQL 或 PostgreSQL。
- `backup`：預留備份服務，後續負責資料庫 dump、檔案備份與保留週期。

## 資料庫建議

目前 `docker-compose.yml` 預留 MySQL 8.4。若後續 API 與資料表設計更適合 PostgreSQL，可在 P3 前改用 PostgreSQL。

## Volume 規劃

- `db_data`：資料庫持久化資料。
- `backup_data`：未來備份輸出位置。
- `upload_data`：若後續有匯入名單、附件或 QR Code 圖檔，可獨立保存。

## .env.example 欄位

- `WEB_PORT`：本機 web 對外 port。
- `APP_ENV`：執行環境，例如 `local`、`staging`、`production`。
- `APP_NAME`：應用名稱。
- `DB_ENGINE`：資料庫引擎，預設 `mysql`。
- `DB_HOST`：資料庫主機，Docker 內預設 `db`。
- `DB_PORT`：資料庫 port。
- `DB_NAME`：資料庫名稱。
- `DB_USER`：資料庫使用者。
- `DB_PASSWORD`：資料庫密碼。
- `DB_ROOT_PASSWORD`：資料庫 root 密碼。
- `BACKUP_RETENTION_DAYS`：備份保留天數。
- `BACKUP_SCHEDULE`：備份排程設定。

## 本機測試啟動方式

```powershell
Copy-Item .env.example .env
docker compose config
docker compose up -d --build
docker compose logs -f
docker compose down
```

若需一併測試資料庫：

```powershell
docker compose --profile db up -d --build
```

## 未來 .240 部署注意事項

- 不得在未經明確指令前部署到 `.240`。
- 部署前需確認 repo、branch、commit、環境變數、volume 路徑、備份策略與 rollback 步驟。
- 部署前需確認不會覆蓋既有服務、port、reverse proxy 或資料庫。
- production 環境不得使用 `.env.example` 的預設密碼。

## Production 保護

目前不得直接動 production，不得連線或修改正式站台資料庫，不得以 production 資料進行未授權測試。

