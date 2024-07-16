---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；RStudio；rstudio；連線到查詢服務；
solution: Experience Platform
title: 將RStudio連線至查詢服務
description: 本檔案將逐步說明連線R Studio與Adobe Experience Platform查詢服務的步驟。
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# 將[!DNL RStudio]連線至查詢服務

本檔案將逐步說明連線[!DNL RStudio]與Adobe Experience Platform [!DNL Query Service]的步驟。

>[!NOTE]
>
> [!DNL RStudio]現在已重新命名為[!DNL Posit]。 [!DNL RStudio]產品已重新命名為[!DNL Posit Connect]、[!DNL Posit Workbench]、[!DNL Posit Package]經理、[!DNL Posit Cloud]和[!DNL Posit Academy]。
>
> 本指南假設您已擁有[!DNL RStudio]的存取權並熟悉其使用方法。 有關[!DNL RStudio]的更多資訊可在[正式 [!DNL RStudio] 檔案](https://rstudio.com/products/rstudio/)中找到。
> 
> 此外，若要搭配查詢服務使用[!DNL RStudio]，您必須安裝[!DNL PostgreSQL] JDBC 4.2驅動程式。 您可以從[[!DNL PostgreSQL] 官方網站](https://jdbc.postgresql.org/download/)下載JDBC驅動程式。

## 在[!DNL RStudio]介面中建立[!DNL Query Service]連線

安裝[!DNL RStudio]之後，您必須安裝RJDBC套件。 如何在官方Post檔案中找到如何透過命令列[連線資料庫](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r)的說明。

如果使用Mac作業系統，您可以從功能表列選取&#x200B;**[!UICONTROL 工具]**，接著從下拉式功能表選取&#x200B;**[!UICONTROL 安裝套件]**。 或者，從RStudio UI選取&#x200B;**[!DNL Packages]**&#x200B;索引標籤，然後選取&#x200B;**[!DNL Install]**。

出現快顯視窗，顯示&#x200B;**[!DNL Install Packages]**&#x200B;畫面。 確定已針對&#x200B;**[!DNL Install from]**&#x200B;區段選取&#x200B;**[!DNL Repository (CRAN)]**。 **[!DNL Packages]**&#x200B;的值應該是`RJDBC`。 請確定已選取&#x200B;**[!DNL Install dependencies]**。 確認所有值正確之後，請選取&#x200B;**[!DNL Install]**&#x200B;以安裝封裝。 現在已安裝RJDBC套件，請重新啟動[!DNL RStudio]以完成安裝程式。

[!DNL RStudio]重新啟動後，您現在可以連線到查詢服務。 在&#x200B;**[!DNL Packages]**&#x200B;窗格中選取&#x200B;**[!DNL RJDBC]**&#x200B;套件，然後在主控台中輸入下列命令：

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

其中`{PATH TO THE POSTGRESQL JDBC JAR}`代表您電腦上安裝的[!DNL PostgreSQL] JDBC JAR路徑。

現在，您可以建立與查詢服務的連線。 在主控台中輸入下列命令：

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>請參閱[[!DNL Query Service] SSL檔案](./ssl-modes.md)，瞭解協力廠商連線至Adobe Experience Platform查詢服務的SSL支援，以及如何使用`verify-full` SSL模式連線。

如需尋找資料庫名稱、主機、連線埠和登入認證的詳細資訊，請參閱[認證指南](../ui/credentials.md)。 若要尋找您的認證，請登入[!DNL Platform]，然後選取&#x200B;**[!UICONTROL 查詢]**，接著選取&#x200B;**[!UICONTROL 認證]**。

主控台輸出中會顯示訊息，確認連線至查詢服務。

## 正在寫入查詢

現在您已連線到[!DNL Query Service]，您可以撰寫查詢以執行及編輯SQL敘述句。 例如，您可以使用`dbGetQuery(con, sql)`來執行查詢，其中`sql`是您要執行的SQL查詢。

下列查詢使用包含[體驗事件](../../xdm/classes/experienceevent.md)的資料集，並依據裝置的熒幕高度建立網站的頁面檢視長條圖。

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

成功的回應會傳回查詢結果：

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

如需如何撰寫和執行查詢的詳細資訊，請閱讀[執行查詢](../best-practices/writing-queries.md)的指南。
