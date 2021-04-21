---
keywords: Experience Platform; home；熱門主題；查詢服務；查詢服務；故障排除指南；常見問題；故障排除；
solution: Experience Platform
title: 查詢服務疑難排解指南
topic-legacy: troubleshooting
description: 本檔案包含您遇到的常見錯誤碼及可能原因的資訊。
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 3%

---

# [!DNL Query Service] 疑難排解指南

## REST API錯誤

| HTTP狀態代碼 | 說明 | 可能的原因 |
| ---------------- | ----------- | --------------- |
| 400 | 錯誤請求 | 格式錯誤或非法查詢 |
| 401 | 驗證失敗 | 驗證Token無效 |
| 500 | 內部伺服器錯誤 | 內部系統故障 |

## PostgreSQL API錯誤

| 錯誤代碼和連接狀態 | 說明 | 可能的原因 |
| ------------------------------- | ----------- | -------------- |
| **28P01** 啟動——身份驗證 | 密碼無效 | 驗證Token無效 |
| **28000** 啟動——驗證 | 授權類型無效 | 授權類型無效。 必須是`AuthenticationCleartextPassword`。 |
| **42P12啟** 動——驗證 | 未找到表 | 未找到要使用的表 |
| **42601查** 詢 | 語法錯誤 | 無效的命令或語法錯誤 |
| **58000查** 詢 | 系統錯誤 | 內部系統故障 |
| **42P01查** 詢 | 找不到表 | 未找到在查詢中指定的表 |
| **42P07查** 詢 | 表存在 | 表已存在同名(CREATE TABLE) |
| **53400查** 詢 | LIMIT超過最大值 | 用戶指定的LIMIT子句高於100,000 |
| **53400查** 詢 | 語句超時 | 提交的即時陳述式最多需要10分鐘 |
| **08P01** N/A | 不支援的訊息類型 | 不支援的訊息類型 |
