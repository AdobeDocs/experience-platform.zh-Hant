---
keywords: Experience Platform；首頁；熱門主題；PSQL;psql；查詢服務；查詢服務；元資料；命令；元資料命令；
solution: Experience Platform
title: 查詢服務中的元資料PostgreSQL命令
description: 目前支援在Adobe Experience Platform查詢服務中查詢元資料的PostgreSQL命令清單。
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# 中繼資料 [!DNL PostgreSQL] 命令

針對資料集的中繼資料，以下 [!DNL PostgreSQL] 當前支援用於查詢的命令：

>[!NOTE]
>
>以下列出的命令區分大小寫。

| 命令 | 說明 |
|------- | ------------|
| `\conninfo` | 輸出有關當前資料庫連接的資訊。 |
| `\d` | 顯示所有可見表、視圖、實體化視圖、序列和外表的清單。 |
| `\dE` | 顯示外表的清單。 |
| `\df or \df+` | 顯示函式清單。 |
| `\di` | 顯示索引清單。 |
| `\dm` | 顯示實體化視圖的清單。 |
| `\dn` | 顯示結構清單（命名空間）。 |
| `\ds` | 顯示序列清單。 |
| `\dS` | 顯示PostgreSQL定義的表的清單。 |
| `\dt` | 顯示表清單。 |
| `\dT` | 顯示資料類型清單。 |
| `\dv` | 顯示視圖清單。 |
| `\encoding` | 列出當前客戶端字元集編碼。 |
| `\errverbose` | 以最大密度重複最新的伺服器錯誤消息。 |
| `\l or \list` | 顯示伺服器中的資料庫清單。 |
| `\set` | 顯示所有當前psql變數的名稱和值。 |
| `\showtables` | 顯示下列資訊： <br>名稱：引用表的名稱。<br>datasetId:儲存的資料集ID。<br>資料集：儲存的資料集名稱。<br>說明：資料集的說明。<br>已解決：指出目前工作階段中是否解析資料集的布林值。 |
| `\timing` | 將顯示切換為開啟和關閉。 顯示單位為毫秒。 超過一秒的間隔以分鐘：秒格式顯示，並視需要新增小時和天欄位。 |

以開頭的所有命令 `\d` 可結合。 例如，您可以 `\dtsn` 顯示所有表、序列和結構的清單。 `\d` 它本身顯示所有可見的表、視圖、實體化視圖和序列。

有關上述命令的其他資訊，請參閱 [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). 但請注意，並非 [!DNL PostgreSQL] 檔案支援 [!DNL Experience Platform].
