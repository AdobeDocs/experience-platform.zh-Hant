---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；RStudio;rstudio；連線至查詢服務；
solution: Experience Platform
title: 將RStudio連接到查詢服務
description: 本檔案將逐步說明將R Studio與Adobe Experience Platform Query Service連接的步驟。
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: d40aa52240ab8f15feea62ec5fb8de073dd6a053
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Connect [!DNL RStudio] 查詢服務

本檔案會逐步說明連接 [!DNL RStudio] 搭配Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> [!DNL RStudio] 現已改名為 [!DNL Posit]. [!DNL RStudio] 產品已重新命名為 [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package] 經理， [!DNL Posit Cloud]，和 [!DNL Posit Academy].
>
> 本指南假設您已擁有 [!DNL RStudio] 並熟悉如何使用。 有關 [!DNL RStudio] 可在 [官方 [!DNL RStudio] 檔案](https://rstudio.com/products/rstudio/).
> 
> 此外，若要使用 [!DNL RStudio] 若使用查詢服務，您必須安裝 [!DNL PostgreSQL] JDBC 4.2驅動程式。 可以從 [[!DNL PostgreSQL] 官方網站](https://jdbc.postgresql.org/download/).

## 建立 [!DNL Query Service] 連線 [!DNL RStudio] 介面

安裝後 [!DNL RStudio]，您需要安裝RJDBC套件。 如何 [通過命令行連接資料庫](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) 可在官方Posit檔案中找到。

如果使用Mac OS，您可以選取 **[!UICONTROL 工具]** 從菜單欄中，後跟 **[!UICONTROL 安裝套件]** 從下拉式功能表。 或者，選取 **[!DNL Packages]** 標籤，然後選取 **[!DNL Install]**.

隨即出現快顯視窗，其中顯示 **[!DNL Install Packages]** 螢幕。 確保 **[!DNL Repository (CRAN)]** 已針對 **[!DNL Install from]** 區段。 的值 **[!DNL Packages]** 應該是 `RJDBC`. 確保 **[!DNL Install dependencies]** 中所有規則的URL。 確認所有值皆正確後，請選取 **[!DNL Install]** 安裝軟體包。 安裝RJDBC包後，重新啟動 [!DNL RStudio] 以完成安裝過程。

之後 [!DNL RStudio] 已重新啟動，您現在可以連線至查詢服務。 選取 **[!DNL RJDBC]** 封裝 **[!DNL Packages]** ，並在控制台中輸入以下命令：

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

其中 `{PATH TO THE POSTGRESQL JDBC JAR}` 代表 [!DNL PostgreSQL] 電腦上安裝的JDBC JAR。

現在，您可以建立與Query Service的連線。 在主控台中輸入下列命令：

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>請參閱 [[!DNL Query Service] SSL檔案](./ssl-modes.md) 了解協力廠商連線至Adobe Experience Platform Query Service的SSL支援，以及如何使用 `verify-full` SSL模式。

有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請閱讀 [認證指南](../ui/credentials.md). 若要尋找憑證，請登入 [!DNL Platform]，然後選取 **[!UICONTROL 查詢]**，後跟 **[!UICONTROL 憑證]**.

主控台輸出中的訊息會確認與查詢服務的連線。

## 寫入查詢

現在您已連線至 [!DNL Query Service]，您可以編寫查詢以執行和編輯SQL陳述式。 例如，您可以使用 `dbGetQuery(con, sql)` 執行查詢，其中 `sql` 是要運行的SQL查詢。

下列查詢使用包含 [體驗事件](../sample-queries/experience-event.md) 並根據裝置的螢幕高度，建立網站的頁面檢視色階分佈圖。

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

## 後續步驟

有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢](../best-practices/writing-queries.md).
