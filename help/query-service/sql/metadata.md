---
keywords: Experience Platform；首頁；熱門主題；PSQL；PSQL；查詢服務；查詢服務；中繼資料；命令；中繼資料命令；
solution: Experience Platform
title: 查詢服務中的中繼資料PostgreSQL命令
description: 目前支援在Adobe Experience Platform查詢服務中查詢中繼資料的PostgreSQL命令清單。
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# 查詢服務中的中繼資料[!DNL PostgreSQL]命令

針對資料集上的中繼資料，目前支援下列[!DNL PostgreSQL]命令進行查詢：

>[!NOTE]
>
>下列命令區分大小寫。

| 命令 | 說明 |
|------- | ------------|
| `\conninfo` | 輸出有關目前資料庫連線的資訊。 |
| `\d` | 顯示所有可見表格、視觀表、具體化視觀表、序列和外部表格的清單。 |
| `\dE` | 顯示外部表格的清單。 |
| `\df or \df+` | 顯示函式清單。 |
| `\di` | 顯示索引清單。 |
| `\dm` | 顯示具體化視觀表的清單。 |
| `\dn` | 顯示結構描述（名稱空間）清單。 |
| `\ds` | 顯示序列清單。 |
| `\dS` | 顯示PostgreSQL定義的表格清單。 |
| `\dt` | 顯示表格清單。 |
| `\dT` | 顯示資料型別清單。 |
| `\dv` | 顯示檢視清單。 |
| `\encoding` | 列出目前的使用者端字元集編碼。 |
| `\errverbose` | 以最大詳細程度重複最近的伺服器錯誤訊息。 |
| `\l or \list` | 顯示伺服器中的資料庫清單。 |
| `\set` | 顯示所有目前psql變數的名稱和值。 |
| `\showtables` | 顯示下列資訊： <br>名稱：參照資料表的名稱。<br>datasetId：儲存的資料集識別碼。<br>資料集：儲存的資料集名稱。<br>說明：資料集的說明。<br>resolved：布林值，表示資料集是否已在目前的工作階段中解析。 |
| `\timing` | 在開啟和關閉顯示之間切換。 顯示單位為毫秒。 超過一秒的間隔會以分鐘：秒的格式顯示，並會視需要新增小時和天欄位。 |

所有以`\d`開頭的命令都可以合併。 例如，您可以發出`\dtsn`以顯示所有表格、序列和結構描述的清單。 `\d`本身會顯示所有可見的表格、視觀表、具體化視觀表和序列。

如需上述命令的其他資訊，請參閱位於[postgresql.org](https://www.postgresql.org/docs/10/app-psql.html)的檔案。 不過，請注意，[!DNL Experience Platform]並不支援[!DNL PostgreSQL]檔案中所顯示的所有選項。
