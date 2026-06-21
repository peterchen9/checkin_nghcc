# GitHub 紀錄

## Repo 名稱

`checkin_nghcc`

## 專案目的

建立「教會智能報到系統」的全新獨立 repo，集中整理前台、後台、Docker 架構、資料庫設計、API 設計、測試、備份與正式部署規劃。

## 初始盤點來源

- 前台參考：https://checkin.nghcc.org.tw/index.html
- 後台參考：https://checkin.nghcc.org.tw/admin.html
- 既有通訊錄來源：http://192.168.16.240:8001
- 使用者提供的功能摘要與安全邊界要求。

目前僅做文件化盤點，不連線或修改正式站台資料庫。通訊錄整合採代理既有服務，不變更 `.240:8001` 原內容。

## Docker 化要求

- 必須使用 Docker 獨立部署。
- `docker-compose.yml` 至少包含 `web` 服務。
- 預留 `db` 與未來 `backup` 規劃。
- 使用 `.env.example` 記錄必要環境變數。
- 本機驗證需至少執行 `docker compose config`，skeleton 可啟動時執行 `docker compose up -d --build`。
- `web` 需提供 `/health` 供容器健康檢查。

## 本次整理紀錄

- QR Code 列印新增 30mm x 30mm 標籤頁。
- Docker/Nginx 新增 `/addressbook/` 代理既有通訊錄。
- 新增 `.dockerignore` 與 compose healthcheck。
- README 與 docs 補上通訊錄與 QR 列印規格。

## 後續階段建議

- 完成 P1 Docker skeleton 驗證。
- 建立 P2 本機開發環境。
- 進行 P3 資料表設計。
- 進行 P4 API 設計。
- 分階段重建前台、後台、Excel 匯出、權限登入、測試與備份。

## 2026-06-21 Docker 功能檢查紀錄

- 修正首頁亂碼與壞掉的 HTML 標籤，補上可用的功能導覽。
- 新增 `admin.html`，避免文件列出的管理台網址進入不存在頁面。
- 修正 QR 標籤列印頁文字，保留 30mm x 30mm 列印版面與 query string 帶入功能。
- 補上 `/contacts/` 與 `/resources/` 代理，讓通訊錄登入頁的 CSS/JS 與表單路徑不會掉回首頁。
- 已確認目前 repo 仍是 Docker skeleton：登入、報到 API、資料庫寫入、Excel 匯出尚未實作。
