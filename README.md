# 教會智能報到系統

`checkin_nghcc` 是「教會智能報到系統」的全新獨立專案 repo，用於整理、盤點、文件化與建立 Docker 化重建基礎。此專案不得影響既有「北門行政作業平台」或其他系統。

## 參考網址

- 前台參考：https://checkin.nghcc.org.tw/index.html
- 後台參考：https://checkin.nghcc.org.tw/admin.html
- 既有通訊錄來源：http://192.168.16.240:8001

以上網址僅作為功能盤點與整合來源。目前不得直接連線或修改正式站台資料庫，也不得部署到 `.240`，除非後續另有明確指令。通訊錄整合採代理方式使用既有服務，不覆寫、不遷移、不修改原內容。

## 功能摘要

前台功能包含主日聚會、成主課程、特別聚會、牧區小組聚會、同工打卡、QR Code 掃描報到、手動搜尋報到，以及同工打卡安全碼驗證。

後台功能包含打卡紀錄查詢、匯出 Excel、課程與活動管理、員工名單管理、通訊錄管理、報名清單、繳費狀態與上課狀況。

目前 skeleton 已整理：

- `src/qr-label-print.html`：QR Code 30x30mm 標籤列印頁。
- `/addressbook/`：透過 Docker/Nginx 代理既有 `192.168.16.240:8001` 通訊錄。
- `/health`：Docker health check endpoint。

## QR Code 30x30mm 標籤列印

本機啟動後開啟：

```text
http://localhost:8080/qr-label-print.html
```

列印頁使用：

- `@page size: 30mm 30mm`
- 標籤外框：30mm x 30mm
- QR 圖片區：21mm x 21mm
- 文字區：6pt，避免超出標籤紙

可用 query string 帶入內容：

```text
/qr-label-print.html?qr=https%3A%2F%2Fexample.com%2Fqr.png&title=主日報到&subtitle=A001
```

實際列印時，印表機與瀏覽器列印設定需確認紙張大小為 30mm x 30mm，邊界為無或 0。

## 通訊錄整合

Docker/Nginx 已設定：

```text
/addressbook/ -> http://192.168.16.240:8001/
```

原則：

- 直接使用既有 `.240:8001` 通訊錄。
- 不修改既有通訊錄內容。
- 不搬移資料、不覆蓋資料、不接正式資料庫寫入。
- 若未來需要 API 寫入或同步，必須另開文件與權限審核。

## Docker 啟動方式

複製環境設定範例：

```powershell
Copy-Item .env.example .env
```

檢查 compose：

```powershell
docker compose config
```

啟動 skeleton：

```powershell
docker compose up -d --build
```

查看 logs：

```powershell
docker compose logs -f
```

停止服務：

```powershell
docker compose down
```

預設本機網址：

```text
http://localhost:8080
```

若要連同預留資料庫服務一起啟動：

```powershell
docker compose --profile db up -d --build
```

## 目錄結構

```text
checkin_nghcc/
  docs/
    admin-feature-inventory.md
    docker-deployment-plan.md
    frontend-feature-inventory.md
    github-record.md
    roadmap.md
    system-overview.md
  docker/
    nginx.conf
  src/
    index.html
    qr-label-print.html
  .dockerignore
  .env.example
  .gitignore
  CHANGELOG.md
  Dockerfile
  README.md
  docker-compose.yml
```

## 開發注意事項

- 本 repo 是全新獨立專案，不可混入其他 repo 的提交。
- 目前工作以盤點、文件化與 Docker skeleton 為主。
- 不要直接修改 production 程式、資料庫或部署設定。
- 不要連線或修改正式站台資料庫。
- 不要部署到 `.240`，除非後續有明確指令。
- 通訊錄只透過 `/addressbook/` 代理使用既有服務，不修改原內容。
- 後續應先建立本機開發環境，再進行資料表、API、前台與後台重建。

## GitHub 紀錄方式

- repo 名稱：`checkin_nghcc`
- 每個階段以清楚中文 commit 記錄。
- 文件、Docker 架構、資料表設計、API 設計、前後台重建與部署規劃皆需保留在 GitHub repo 內。
- 正式站台相關資訊只能作為盤點來源，不得在未確認安全邊界前加入敏感憑證或 production 資料。
