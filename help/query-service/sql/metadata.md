---
keywords: Experience Platform;home；常用主題；PSQL;psql；查詢服務；查詢服務；元資料；命令；元資料命令；
solution: Experience Platform
title: 查詢服務中的元資料PostgreSQL命令
topic-legacy: metadata
description: 當前支援查詢Adobe Experience Platform查詢服務中元資料的PostgreSQL命令清單。
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 查詢服務中的元資料PostgreSQL命令

對於資料集上的元資料，當前支援查詢以下PostgreSQL命令：

>[!NOTE]
>
>下面列出的命令區分大小寫。

| 命令 | 說明 |
|------- | ------------|
| `\conninfo` | 輸出有關當前資料庫連接的資訊。 |
| `\d` | 顯示所有可見表、視圖、實體化視圖、序列和外表的清單。 |
| `\dE` | 顯示外表的清單。 |
| `\df or \df+` | 顯示函式清單。 |
| `\di` | 顯示索引清單。 |
| `\dm` | 顯示實體化視圖的清單。 |
| `\dn` | 顯示結構（名稱空間）的清單。 |
| `\ds` | 顯示序列清單。 |
| `\dS` | 顯示PostgreSQL定義的表的清單。 |
| `\dt` | 顯示表的清單。 |
| `\dT` | 顯示資料類型清單。 |
| `\dv` | 顯示視圖清單。 |
| `\encoding` | 列出當前客戶機字元集編碼。 |
| `\errverbose` | 以最大詳細程度重複最近的伺服器錯誤消息。 |
| `\l or \list` | 顯示伺服器中的資料庫清單。 |
| `\set` | 顯示所有當前psql變數的名稱和值。 |
| `\showtables` | 顯示下列資訊：<br>name:引用表的名稱。<br>datasetId:儲存的資料集的ID。<br>資料集：儲存的資料集名稱。<br>說明：資料集的說明。<br>已解決：一個布爾值，用於指示當前會話中是否解析資料集。 |
| `\timing` | 在開啟和關閉之間切換顯示。 顯示以毫秒為單位。 超過一秒的間隔以分鐘：秒格式顯示，並視需要新增小時和天欄位。 |

所有以`\d`開頭的命令都可以合併。 例如，您可以發佈`\dtsn`來顯示所有表、序列和方案的清單。 `\d` 單獨顯示所有可見表、視圖、實體化視圖和序列。

有關上述命令的其他資訊，請參閱[postgresql.org](https://www.postgresql.org/docs/10/app-psql.html)中的文檔。 但是，請注意，並非[!DNL Experience Platform]支援PostgreSQL文檔中顯示的所有選項。
