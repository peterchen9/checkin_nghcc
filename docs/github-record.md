# GitHub 紀錄

## Repo 名稱

`checkin_nghcc`

## 專案目的

建立「教會智能報到系統」的全新獨立 repo，集中整理前台、後台、Docker 架構、資料庫設計、API 設計、測試、備份與正式部署規劃。

## 初始盤點來源

- 前台參考：https://checkin.nghcc.org.tw/index.html
- 後台參考：https://checkin.nghcc.org.tw/admin.html
- 使用者提供的功能摘要與安全邊界要求。

目前僅做文件化盤點，不連線或修改正式站台資料庫。

## Docker 化要求

- 必須使用 Docker 獨立部署。
- `docker-compose.yml` 至少包含 `web` 服務。
- 預留 `db` 與未來 `backup` 規劃。
- 使用 `.env.example` 記錄必要環境變數。
- 本機驗證需至少執行 `docker compose config`，skeleton 可啟動時執行 `docker compose up -d --build`。

## 後續階段建議

- 完成 P1 Docker skeleton 驗證。
- 建立 P2 本機開發環境。
- 進行 P3 資料表設計。
- 進行 P4 API 設計。
- 分階段重建前台、後台、Excel 匯出、權限登入、測試與備份。

