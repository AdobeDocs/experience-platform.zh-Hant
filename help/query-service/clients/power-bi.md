---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；Power BI;power bi；連線至查詢服務；
solution: Experience Platform
title: 將Power BI連接到查詢服務
topic-legacy: connect
description: 本檔案會逐步說明將Power BI與Adobe Experience Platform Query Service連線的步驟。
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 1%

---

# Connect [!DNL Power BI] 查詢服務

本檔案涵蓋連接 [!DNL Power BI] 具有Adobe Experience Platform查詢服務的案頭。

## 快速入門

本指南要求您已具備 [!DNL Power BI] 案頭應用程式，熟悉如何導覽其介面。 若要下載 [!DNL Power BI] 案頭或如需詳細資訊，請參閱 [官方 [!DNL Power BI] 檔案](https://docs.microsoft.com/zh-tw/power-bi/).

>[!IMPORTANT]
>
> 此 [!DNL Power BI] 案頭應用程式 **僅限** 可在Windows裝置上使用。

獲取連接所需的憑據 [!DNL Power BI] 若要Experience Platform，您必須擁有平台UI中查詢工作區的存取權。 如果您目前沒有查詢工作區的存取權，請連絡您的IMS組織管理員。

安裝後 [!DNL Power BI]，您需要安裝 `Npgsql`，是PostgreSQL的.NET驅動程式包。 有關Npgsql的更多資訊，請參見 [Npgsql文檔](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>您必須下載v4.0.10或更低版本，因為較新版本會導致錯誤。

在「[!DNL Npgsql GAC Installation]「自訂設定」畫面上，選取 **[!DNL Will be installed on local hard drive]**.

要確保已正確安裝Npgsql，請先重新啟動電腦，然後再繼續執行後續步驟。

## Connect [!DNL Power BI] 查詢服務 {#connect-power-bi}

連接 [!DNL Power BI] 至查詢服務，開啟 [!DNL Power BI] 選取 **[!DNL Get Data]** 功能表功能區中。

![此 [!DNL Power BI] 反白顯示資料的控制面板首頁標籤。](../images/clients/power-bi/open-power-bi.png)

輸入&quot;[!DNL PostgreSQL]」，縮小資料來源清單。 在顯示的結果下，選取 **[!DNL PostgreSQL database]**，後跟 **[!DNL Connect]**.

![取得資料對話方塊 [!DNL PostgreSQL] 資料庫和連接突出顯示。](../images/clients/power-bi/get-data.png)

此 [!DNL PostgreSQL] 資料庫對話框出現，請求伺服器和資料庫的值。 這些值取自您的Adobe Experience Platform憑證。 若要尋找憑證，請登入Platform UI並選取 **[!UICONTROL 查詢]** 從左側導覽，後跟 **[!UICONTROL 憑證]**. 有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請閱讀 [認證指南](../ui/credentials.md).

![「Experience Platform查詢」工作區，其中「憑證」索引標籤和「即將到期」憑證已反白顯示。](../images/clients/power-bi/query-service-credentials-page.png)

若 **[!DNL Server]** 在「Power BI」欄位中，為在「查詢服務憑據」部分中找到的主機輸入值。 針對生產環境，添加埠 `:80` 到主機字串的結尾。 例如 `made-up.platform-query.adobe.io:80`。

此 **[!DNL Database]** 欄位可以是「all」或資料集表格名稱。 例如 `prod:all`。

>[!IMPORTANT]
>
>第三方BI工具中的巢狀資料結構可以平面化，以改善其可用性，並減少擷取、分析、轉換和報告資料所需的工作量。 請參閱[`FLATTEN` 功能](../best-practices/flatten-nested-data.md) 有關在連接到資料庫時如何激活此設定的說明。

![此 [!DNL Power BI] 儀表板，其中突出顯示了伺服器和資料庫輸入欄位。](../images/clients/power-bi/postgresql-database-dialog.png)

### 資料連接模式

接下來，您可以選取 **[!DNL Data Connectivity mode]**. 選擇 **[!DNL Import]** 後跟 **[!DNL OK]** 顯示所有可用表的清單，或選擇 **[!DNL DirectQuery]** 直接查詢資料源，而不直接將資料導入或複製到 [!DNL Power BI].

若要深入了解 **[!DNL Import]** 模式，請閱讀 [導入表](#import). 若要深入了解 **[!DNL DirectQuery]** 模式，請閱讀 [在不匯入資料的情況下查詢資料集](#direct-query).

選擇 **[!DNL OK]** 確認資料庫詳細資訊後。

![此 [!DNL PostgreSQL] 資料庫對話框，「資料連接」模式突出顯示。](../images/clients/power-bi/connectivity-mode.png)

### 驗證

系統會顯示詢問您的使用者名稱、密碼和應用程式設定的提示。 在此案例中，使用者名稱為您的組織ID，密碼為驗證Token。 在「查詢服務」憑據頁上可以找到這兩者。

填寫這些詳細資訊，然後選取 **[!DNL Connect]** 繼續下一步。

![資料庫對話框中突出顯示了用戶名、密碼和應用程式設定下拉菜單。](../images/clients/power-bi/import-mode.png)

## 匯入表格 {#import}

選取 **[!DNL Import]** [!DNL Data Connectivity mode]，則會匯入完整資料集，以便您在 [!DNL Power BI] 案頭應用程式原樣。

>[!IMPORTANT]
>
>若要查看自初次匯入後發生的資料變更，您必須在內重新整理資料 [!DNL Power BI] 重新匯入完整資料集。

要導入表，請輸入伺服器和資料庫詳細資訊 [如上所述](#connect-power-bi) ，然後選取 **[!DNL Import]** [!DNL Data Connectivity mode]，後跟 **[!DNL OK]**. 此時將出現一個對話框，顯示所有可用表的清單。 選擇要預覽的表，後面跟 **[!DNL Load]** 將資料集帶入Power BI。

![帶有表的「導航」對話框，並突出顯示「載入」。](../images/clients/power-bi/preview-table.png)

表格現在已匯入 [!DNL Power BI].

![此 [!DNL Power BI] 加亮顯示建立自訂視覺效果指示的控制面板。](../images/clients/power-bi/import-table.png)

### 使用自定義SQL導入表

[!DNL Power BI] 和其他協力廠商工具（例如Tableau）目前不允許使用者匯入巢狀物件，例如Platform中的XDM物件。 為了解釋這個， [!DNL Power BI] 可讓您使用自訂SQL來存取這些巢狀欄位，並建立資料的平面化檢視。 [!DNL Power BI] 然後，將先前嵌套資料的此平面化視圖作為普通表載入。

從 [!DNL PostgreSQL] 資料庫彈出窗口，選擇 **[!DNL Advanced options]** 要在 **[!DNL SQL statement]** 區段。 此自訂查詢應用來將JSON名稱值配對平面化為表格格式。

![此 [!DNL PostgreSQL] 資料庫對話框，其中突出顯示了資料連接模式高級選項。 這允許您建立自定義SQL陳述式。](../images/clients/power-bi/custom-sql-statement.png)

輸入自定義查詢後，請選擇 **[!DNL OK]** 繼續連接資料庫。 請參閱 [驗證](#authentication) 以取得從工作流程的這個部分連接資料庫的指引。

驗證完成後，平面化資料的預覽會顯示在 [!DNL Power BI] 案頭儀表板作為表。 伺服器和資料庫名稱列在對話框的頂部。 選擇 **[!DNL Load]** 來完成匯入程式。

![中平面化、匯入表格的視覺效果 [!DNL Power BI] 控制面板。](../images/clients/power-bi/imported-table-preview.png)

視覺效果現在可供編輯和匯出 [!DNL Power BI] 案頭應用程式。

## 查詢資料集而不匯入資料 {#direct-query}

此 **[!DNL DirectQuery]** [!DNL Data Connectivity mode] 直接查詢資料源，而不將資料匯入或複製到 [!DNL Power BI] 案頭。 使用此連線模式，您可以透過UI，以目前資料重新整理所有視覺效果。 不過，產生或重新整理視覺效果所需的時間會因基礎資料來源的效能而異。

若要使用 [!DNL Data Connectivity mode]，請選取 **[!DNL DirectQuery]** 切換 **[!DNL Advanced options]** 要在 **[!DNL SQL statement]** 區段。 確保 **[!DNL Include relationship columns]** 中所有規則的URL。 完成查詢後，請選擇 **[!DNL OK]** 繼續。

![此 [!DNL PostgreSQL] 資料庫對話框，其中突出顯示了使用資料連接模式所需的設定。](../images/clients/power-bi/direct-query-mode.png)

查詢的預覽隨即顯示。 選擇 **[!DNL Load]** ，查看查詢結果。

![範例查詢的表格化結果預覽。](../images/clients/power-bi/preview-direct-query.png)

## 後續步驟

閱讀本檔案後，您現在應了解如何連線至 [!DNL Power BI] 案頭應用程式和不同的資料連接模式。 有關如何寫入和運行查詢的詳細資訊，請參閱 [查詢執行指南](../best-practices/writing-queries.md).
