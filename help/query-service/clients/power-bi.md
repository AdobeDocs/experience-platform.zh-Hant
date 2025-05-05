---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；Power BI；power bi；連線到查詢服務；
solution: Experience Platform
title: 將Power BI連線至查詢服務
description: 本檔案將逐步說明連線Power BI與Adobe Experience Platform查詢服務的步驟。
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# 將[!DNL Power BI]連線至查詢服務

本檔案說明將[!DNL Power BI]案頭連線至Adobe Experience Platform查詢服務的步驟。

## 快速入門

本指南要求您已存取[!DNL Power BI]案頭應用程式，並熟悉如何導覽其介面。 若要下載[!DNL Power BI]案頭或如需詳細資訊，請參閱[正式 [!DNL Power BI] 檔案](https://docs.microsoft.com/en-us/power-bi/)。

>[!IMPORTANT]
>
> [!DNL Power BI]案頭應用程式&#x200B;**僅限**&#x200B;可在Windows裝置上使用。

若要取得將[!DNL Power BI]連線到Experience Platform所需的認證，您必須能存取Experience Platform UI中的查詢工作區。 如果您目前沒有查詢工作區的存取權，請聯絡您的組織管理員。

## 將[!DNL Power BI]連線至查詢服務 {#connect-power-bi}

若要將[!DNL Power BI]連線至查詢服務，請開啟[!DNL Power BI]並在頂端功能表功能區中選取&#x200B;**[!DNL Get Data]**。 接著，在搜尋列中輸入&quot;[!DNL PostgreSQL]&quot;以縮小資料來源清單。 從顯示的結果中，選取&#x200B;**[!DNL PostgreSQL database]**，然後選取&#x200B;**[!DNL Connect]**。

[!DNL PostgreSQL]資料庫對話方塊隨即顯示，要求伺服器和資料庫的值。 有關如何[從Power Query Desktop](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop)連線至PostgreSQL資料庫的其他說明，請參閱官方[!DNL PowerBI]檔案。

這些必要的值會從您的Adobe Experience Platform憑證中取得。 若要尋找您的認證，請登入Experience Platform UI，然後從左側導覽選取&#x200B;**[!UICONTROL 查詢]**，接著選取&#x200B;**[!UICONTROL 認證]**。 如需尋找資料庫名稱、主機、連線埠和登入認證的詳細資訊，請參閱[認證指南](../ui/credentials.md)。

>[!IMPORTANT]
>
>身為Power BI或Tableau使用者，您可以從查詢服務憑證標籤將Customer Journey Analytics連線至您的BI工具。 請參閱認證檔案，瞭解如何[將您的BI工具連線至Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics)的說明。

![Experience Platform查詢工作區的[認證]索引標籤和[過期]認證已反白顯示。](../images/clients/power-bi/query-service-credentials-page.png)

在[!DNL PostgreSQL database]對話方塊的&#x200B;**[!DNL Server]**&#x200B;欄位中，輸入在查詢服務[!UICONTROL 認證]區段中找到之主機的值。 對於生產，請將連線埠`:80`新增到主機字串的結尾。 例如 `made-up.platform-query.adobe.io:80`。

**[!DNL Database]**&#x200B;欄位可以是「all」或資料集表格名稱。 例如 `prod:all`。

>[!IMPORTANT]
>
>第三方BI工具中的巢狀資料結構可以平面化，以提高其可用性，並減少擷取、分析、轉換和報表資料所需的工作量。 請參閱[`FLATTEN`功能](../key-concepts/flatten-nested-data.md)的相關檔案，瞭解連線至資料庫時如何啟用此設定的說明。

### 資料連線模式 {#data-connectivity-mode}

接下來，您可以選取您的&#x200B;**[!DNL Data Connectivity mode]**。 在[!DNL PostgreSQL database]對話方塊中，選取&#x200B;**[!DNL Import]**，然後選取&#x200B;**[!DNL OK]**&#x200B;以顯示所有可用資料表的清單，或選取&#x200B;**[!DNL DirectQuery]**&#x200B;直接查詢資料來源，而不將資料直接匯入或複製到[!DNL Power BI]。

若要深入瞭解&#x200B;**[!DNL Import]**&#x200B;模式，請閱讀[匯入資料表](#import)的章節。 若要深入瞭解&#x200B;**[!DNL DirectQuery]**&#x200B;模式，請閱讀[查詢資料集但不匯入資料](#direct-query)的區段。

在確認您的資料庫詳細資料之後，選取&#x200B;**[!DNL OK]**。

### Authentication {#authentication}

確認您的資料連線模式後，畫面會顯示提示，詢問您的使用者名稱、密碼和應用程式設定。 在此案例中，使用者名稱是您的組織ID，密碼是您的驗證Token。 兩者皆可在「查詢服務認證」頁面上找到。

填寫這些詳細資料，然後選取「**[!DNL Connect]**」以繼續下一個步驟。

## 匯入表格 {#import}

透過選取&#x200B;**[!DNL Import]** [!DNL Data Connectivity mode]，已匯入完整資料集，這可讓您以原樣使用[!DNL Power BI]案頭應用程式中選取的表格和欄。

>[!IMPORTANT]
>
>若要檢視自初始匯入後發生的資料變更，您必須重新匯入完整資料集，重新整理[!DNL Power BI]內的資料。

若要匯入資料表，請輸入伺服器和資料庫詳細資訊[，如上所述](#connect-power-bi)，然後選取&#x200B;**[!DNL Import]** [!DNL Data Connectivity mode]，接著選取&#x200B;**[!DNL OK]**。 [!DNL Navigator]對話方塊隨即顯示，顯示所有可用表格的清單。 選取您要預覽的資料表，接著選取&#x200B;**[!DNL Load]**&#x200B;以將資料集匯入Power BI。 資料表現在已匯入[!DNL Power BI]。

[在官方檔案中可找到有關連線至PowerBi案頭應用程式中資料的一般資訊](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data)。

### 使用自訂SQL匯入表格

[!DNL Power BI]和其他協力廠商工具（例如[!DNL Tableau]）目前不允許使用者匯入巢狀物件，例如Experience Platform中的XDM物件。 若要解決此問題，[!DNL Power BI]可讓您使用自訂SQL來存取這些巢狀欄位，並建立資料的平面化檢視。 [!DNL Power BI]接著會將先前巢狀資料的這個平面化檢視載入為一般表格。

從[!DNL PostgreSQL database]對話方塊中，選取&#x200B;**[!DNL Advanced options]**&#x200B;以在&#x200B;**[!DNL SQL statement]**&#x200B;區段中輸入自訂SQL查詢。 此自訂查詢可用來將JSON名稱值配對平面化為表格格式。 官方檔案也提供如何在進階選項[&#128279;](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options)中使用SQL陳述式連線PowerBI的資訊。

輸入自訂查詢後，選取&#x200B;**[!DNL OK]**&#x200B;以繼續連線資料庫。 請參閱上面的[驗證](#authentication)一節，以取得從工作流程的這個部分連線資料庫的指南。

驗證完成後，平面化資料的預覽會顯示在[!DNL Power BI]案頭儀表板中，做為表格。 伺服器和資料庫名稱會列在對話方塊的頂端。 選取&#x200B;**[!DNL Load]**&#x200B;以完成匯入程式。

視覺效果現在可以從[!DNL Power BI]案頭應用程式進行編輯和匯出。

## 查詢資料集而不匯入資料 {#direct-query}

**[!DNL DirectQuery]** [!DNL Data Connectivity mode]直接查詢資料來源，而不將資料匯入或複製到[!DNL Power BI]案頭。 使用此連線模式，您可以透過UI以目前資料重新整理所有視覺效果。 不過，產生或重新整理視覺效果所需的時間會因基礎資料來源的效能而異。

有關[使用 [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery)的更多資訊，以及其[連線選項、使用案例和限制](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about)的完整討論，可在官方[!DNL PowerBI]檔案中找到。

若要使用此[!DNL Data Connectivity mode]，請選取&#x200B;**[!DNL DirectQuery]**&#x200B;切換，然後選取&#x200B;**[!DNL Advanced options]**，以在&#x200B;**[!DNL SQL statement]**&#x200B;區段中輸入自訂SQL查詢。 確定已選取&#x200B;**[!DNL Include relationship columns]**。 完成查詢之後，請選取&#x200B;**[!DNL OK]**&#x200B;以繼續。

您的查詢預覽隨即顯示。 選取&#x200B;**[!DNL Load]**&#x200B;以檢視查詢的結果。

## 後續步驟

閱讀本檔案後，您現在應該瞭解如何連線至[!DNL Power BI]案頭應用程式，以及可用的不同資料連線模式。 如需如何撰寫和執行查詢的詳細資訊，請參閱查詢執行的[指南](../best-practices/writing-queries.md)。
