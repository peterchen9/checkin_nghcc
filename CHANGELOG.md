# CHANGELOG

## 2026-06-20

- 新增 QR Code 30mm x 30mm 標籤列印頁。
- 新增 `/addressbook/` Nginx 代理，直接使用既有 `192.168.16.240:8001` 通訊錄且不修改原內容。
- 重整 Docker Compose，加入專案名稱、healthcheck 與 `.dockerignore`。
- 更新 README 與文件，記錄 QR 列印規格、通訊錄整合與 Docker/GitHub 維護方式。

## 2026-06-02

- 建立 `checkin_nghcc` 獨立專案骨架。
- 新增 Docker skeleton，包含 `web` 服務與預留 `db` 服務。
- 新增初始盤點文件與部署規劃文件。
