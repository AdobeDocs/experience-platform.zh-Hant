---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；RStudio;rstudio；連接到查詢服務；
solution: Experience Platform
title: 將RStudio連接到查詢服務
description: 本文檔介紹將R Studio與Adobe Experience Platform查詢服務連接的步驟。
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 連接 [!DNL RStudio] 查詢服務

本文檔介紹了連接的步驟 [!DNL RStudio] 與Adobe Experience Platform [!DNL Query Service]。

>[!NOTE]
>
> [!DNL RStudio] 現在被重新標為 [!DNL Posit]。 [!DNL RStudio] 產品已更名為 [!DNL Posit Connect]。 [!DNL Posit Workbench]。 [!DNL Posit Package] 經理， [!DNL Posit Cloud], [!DNL Posit Academy]。
>
> 本指南假定您已具有訪問 [!DNL RStudio] 並熟悉如何使用。 有關 [!DNL RStudio] 在 [官 [!DNL RStudio] 文檔](https://rstudio.com/products/rstudio/)。
> 
> 此外，要使用 [!DNL RStudio] 使用Query Service時，需要安裝 [!DNL PostgreSQL] JDBC 4.2驅動程式。 可以從 [[!DNL PostgreSQL] 官方網站](https://jdbc.postgresql.org/download/)。

## 建立 [!DNL Query Service] 連接 [!DNL RStudio] 介面

安裝後 [!DNL RStudio]，需要安裝RJDBC包。 有關如何 [通過命令行連接資料庫](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) 可以在官方的Posit檔案中找到。

如果使用Mac作業系統，可以選擇 **[!UICONTROL 工具]** 按 **[!UICONTROL 安裝包]** 的下界。 或者，選擇 **[!DNL Packages]** 頁籤，然後選擇 **[!DNL Install]**。

出現一個彈出窗口，顯示 **[!DNL Install Packages]** 的上界。 確保 **[!DNL Repository (CRAN)]** 為 **[!DNL Install from]** 的子菜單。 的值 **[!DNL Packages]** 應該 `RJDBC`。 確保 **[!DNL Install dependencies]** 的子菜單。 確認所有值均正確後，選擇 **[!DNL Install]** 安裝軟體包。 RJDBC包已安裝，請重新啟動 [!DNL RStudio] 完成安裝過程。

之後 [!DNL RStudio] 已重新啟動，您現在可以連接到查詢服務。 選擇 **[!DNL RJDBC]** 包 **[!DNL Packages]** ，然後在控制台中輸入以下命令：

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

位置 `{PATH TO THE POSTGRESQL JDBC JAR}` 表示到 [!DNL PostgreSQL] 已安裝在電腦上的JDBC JAR。

現在，您可以建立與查詢服務的連接。 在控制台中輸入以下命令：

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>查看 [[!DNL Query Service] SSL文檔](./ssl-modes.md) 瞭解對與Adobe Experience Platform查詢服務的第三方連接的SSL支援，以及如何使用 `verify-full` SSL模式。

有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請閱讀 [憑據指南](../ui/credentials.md)。 要查找憑據，請登錄到 [!DNL Platform]，然後選擇 **[!UICONTROL 查詢]**，後跟 **[!UICONTROL 憑據]**。

控制台輸出中的一條消息確認與查詢服務的連接。

## 寫入查詢

現在您已連接到 [!DNL Query Service]，您可以編寫查詢以執行和編輯SQL陳述式。 例如，您可以 `dbGetQuery(con, sql)` 執行查詢，其中 `sql` 是要運行的SQL查詢。

以下查詢使用包含 [體驗事件](../../xdm/classes/experienceevent.md) 並根據設備的螢幕高度建立網站頁面視圖的直方圖。

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

成功的響應返回查詢結果：

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

有關如何編寫和運行查詢的詳細資訊，請閱讀上的指南 [運行查詢](../best-practices/writing-queries.md)。
