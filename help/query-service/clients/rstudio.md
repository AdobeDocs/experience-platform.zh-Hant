---
keywords: Experience Platform;home;popular topics;Query service;query service;RStudio;rstudio;connect to query service;
solution: Experience Platform
title: 使用RStudio連線
topic: connect
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 2%

---


# 連接 [!DNL RStudio]

本檔案將逐步說明如何將R Studio與Adobe Experience Platform連接 [!DNL Query Service]。

在安裝 [!DNL RStudio]後，在出現的 *Console* （控制台）畫面上，您首先需要準備R指令碼才能使用 [!DNL PostgreSQL]。

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

在準備好R指令碼使用後 [!DNL PostgreSQL]，您現在可以通過加 [!DNL RStudio] 載驅 [!DNL Query Service] 動程式連接 [!DNL PostgreSQL] 到。

```r
drv <- dbDriver("PostgreSQL")
con <- dbConnect(drv, 
 dbname = "{DATABASE_NAME}",
 host="{HOST_NUMBER}",
 port={PORT_NUMBER},
 user="{USERNAME}",
 password="{PASSWORD}")
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{DATABASE_NAME}` | 將使用的資料庫的名稱。 |
| `{HOST_NUMBER` 和 `{PORT_NUMBER}` | 查詢服務的主機端點及其埠。 |
| `{USERNAME}` 和 `{PASSWORD}` | 將使用的登錄憑據。 用戶名的形式為 `ORG_ID@AdobeOrg`。 |

>[!NOTE]
>
>有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請訪問平台 [上的憑據頁](https://platform.adobe.com/query/configuration)。 若要尋找您的認證，請登入，按一 [!DNL Platform]下「查 **[!UICONTROL 詢]**」，然後按一 **[!UICONTROL 下「認證]**」。

## 後續步驟

現在您已連接到 [!DNL Query Service]，您可以編寫查詢以執行和編輯SQL陳述式。 例如，您可以使 `dbGetQuery(con, sql)` 用執行查詢，其 `sql` 中是要運行的SQL查詢。

下列查詢使用包含 [ExperienceEvents的資料集](../creating-queries/experience-event-queries.md) ，並根據裝置的螢幕高度建立網站頁面檢視的色階分佈圖。

```sql
df_pageviews <- dbGetQuery(con,
"SELECT t.range AS buckets, 
 Count(*) AS pageviews 
FROM (SELECT CASE 
 WHEN device.screenheight BETWEEN 0 AND 99 THEN '0 - 99' 
 WHEN device.screenheight BETWEEN 100 AND 199 THEN '100-199' 
 WHEN device.screenheight BETWEEN 200 AND 299 THEN '200-299' 
 WHEN device.screenheight BETWEEN 300 AND 399 THEN '300-399' 
 WHEN device.screenheight BETWEEN 400 AND 499 THEN '400-499' 
 WHEN device.screenheight BETWEEN 500 AND 599 THEN '500-599' 
 ELSE '600-699' 
 end AS range 
 FROM aa_post_vals_3) t 
GROUP BY t.range 
ORDER BY buckets 
LIMIT 1000000")
```

成功的回應會傳回查詢的結果：

```r
df_pageviews
 buckets pageviews
1 0 - 99 198985
2 500-599 67138
3 300-399 2147
4 200-299 354
5 400-499 6947
6 100-199 4415
7 600-699 3097040
```

有關如何編寫和運行查詢的詳細資訊，請閱讀運行查 [詢指南](../creating-queries/creating-queries.md)。