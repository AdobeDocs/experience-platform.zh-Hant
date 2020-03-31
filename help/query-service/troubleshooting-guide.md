---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform查詢服務疑難排解指南
topic: troubleshooting
translation-type: tm+mt
source-git-commit: c5bb112220b40fa6c2adfa89c80ddb87d382fbda

---


# 錯誤和疑難排解

## REST API錯誤

| HTTP狀態代碼 | 說明 | 可能的原因 |
| ---------------- | ----------- | --------------- |
| 400 | 錯誤請求 | 格式錯誤或非法查詢 |
| 401 | 驗證失敗 | 驗證Token無效 |
| 500 | 內部伺服器錯誤 | 內部系統故障 |

## PostgreSQL API錯誤

| 錯誤代碼和連接狀態 | 說明 | 可能的原因 |
| ------------------------------- | ----------- | -------------- |
| **28P01啟動** -身份驗證 | 密碼無效 | 驗證Token無效 |
| **28000** Start-up —— 身份驗證 | 授權類型無效 | 授權類型無效。 一定是 `AuthenticationCleartextPassword`。 |
| **42P12** 啟動——身份驗證 | 未找到表 | 未找到要使用的表 |
| **小行星** 42601 | 語法錯誤 | 無效的命令或語法錯誤 |
| **58000** Query | 系統錯誤 | 內部系統故障 |
| **42P01查詢** | 找不到表 | 未找到在查詢中指定的表 |
| **42P07查詢** | 表存在 | 表已存在同名(CREATE TABLE) |
| **53400** Query | LIMIT超過最大值 | 用戶指定的LIMIT子句高於100,000 |
| **53400** Query | 語句超時 | 提交的即時陳述式最多需要10分鐘 |
| **08P01** N/A | 不支援的訊息類型 | 不支援的訊息類型 |
