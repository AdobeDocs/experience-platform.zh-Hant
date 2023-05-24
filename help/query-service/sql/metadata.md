---
keywords: Experience Platform；首頁；熱門主題；PSQL;psql；查詢服務；查詢服務；元資料；命令；元資料命令；
solution: Experience Platform
title: 查詢服務中的元資料PostgreSQL命令
description: 當前支援查詢Adobe Experience Platform查詢服務中元資料的PostgreSQL命令清單。
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# 元資料 [!DNL PostgreSQL] 查詢服務中的命令

對於資料集上的元資料，以下 [!DNL PostgreSQL] 當前支援用於查詢的命令：

>[!NOTE]
>
>下面列出的命令區分大小寫。

| 命令 | 說明 |
|------- | ------------|
| `\conninfo` | 輸出有關當前資料庫連接的資訊。 |
| `\d` | 顯示所有可見表、視圖、實體化視圖、序列和外來表的清單。 |
| `\dE` | 顯示外來表的清單。 |
| `\df or \df+` | 顯示函式清單。 |
| `\di` | 顯示索引清單。 |
| `\dm` | 顯示實例化視圖的清單。 |
| `\dn` | 顯示架構（命名空間）的清單。 |
| `\ds` | 顯示序列清單。 |
| `\dS` | 顯示PostgreSQL定義的表的清單。 |
| `\dt` | 顯示表清單。 |
| `\dT` | 顯示資料類型清單。 |
| `\dv` | 顯示視圖清單。 |
| `\encoding` | 列出當前客戶端字元集編碼。 |
| `\errverbose` | 以最大詳細程度重複最近的伺服器錯誤消息。 |
| `\l or \list` | 顯示伺服器中的資料庫清單。 |
| `\set` | 顯示所有當前psql變數的名稱和值。 |
| `\showtables` | 顯示以下資訊： <br>名稱：引用表的名稱。<br>資料集ID:儲存的資料集的ID。<br>資料集：儲存的資料集的名稱。<br>說明：資料集的說明。<br>已解決：一個布爾值，用於說明當前會話中是否解析了資料集。 |
| `\timing` | 在開啟和關閉之間切換顯示。 顯示以毫秒為單位。 超過一秒的間隔以分鐘：秒格式顯示，並在需要時添加小時和天欄位。 |

所有以 `\d` 可以合併。 例如，您可以 `\dtsn` 顯示所有表、序列和方案的清單。 `\d` 僅顯示所有可見的表、視圖、實體化視圖和序列。

有關上述命令的其他資訊，請參閱以下文檔： [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html)。 但是，請注意，並非在 [!DNL PostgreSQL] 文檔由 [!DNL Experience Platform]。
