---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；Power BI；電源；連接到查詢服務；
solution: Experience Platform
title: 將Power BI連接到查詢服務
topic-legacy: connect
description: 本文檔將介紹與Adobe Experience Platform查詢服務連接Power BI的步驟。
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 0c20b19c4c34b29c46964d5d87a8646c61055b06
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# 將Power BI連接到查詢服務

本文檔介紹將Power BI案頭與Adobe Experience Platform查詢服務連接的步驟。

## 快速入門

本指南要求您已經具有訪問Power BI案頭應用的權限，並熟悉如何導航其介面。 要下載Power BI案頭或瞭解詳細資訊，請參閱 [官方Power BI檔案](https://docs.microsoft.com/zh-tw/power-bi/)。

>[!IMPORTANT]
>
> Power BI案頭應用程式 **僅** 在Windows設備上可用。

要獲取將Power BI連接到Experience Platform所需的憑據，您必須有權訪問平台UI中的「查詢」工作區。 如果您當前沒有訪問查詢工作區的權限，請與IMS組織管理員聯繫。

安裝Power BI後，需要安裝 `Npgsql`，用於PostgreSQL的.NET驅動程式包。 有關Npgsql的詳細資訊，請參見 [Npgsql文檔](https://www.npgsql.org/doc/index.html)。

>[!IMPORTANT]
>
>您必須下載v4.0.10或更低版本，因為較新版本會導致錯誤。

在「」下[!DNL Npgsql GAC Installation]&quot;在自定義設定螢幕上，選擇 **[!DNL Will be installed on local hard drive]**。

要確保Npgsql已正確安裝，請在繼續執行後續步驟之前重新啟動電腦。

## 將Power BI連接到查詢服務 {#connect-power-bi}

要將Power BI連接到查詢服務，請開啟Power BI並選擇 **[!DNL Get Data]** 的子菜單。

![](../images/clients/power-bi/open-power-bi.png)

在搜索欄中輸入「PostgreSQL」以縮小資料源清單。 在顯示的結果下，選擇 **[!DNL PostgreSQL database]**，後跟 **[!DNL Connect]**。

![](../images/clients/power-bi/get-data.png)

此時將顯示PostgreSQl資料庫對話框，請求伺服器和資料庫的值。 這些值取自您的Adobe Experience Platform憑據。 要查找憑據，請登錄到平台UI並選擇 **[!UICONTROL 查詢]** 從左導航，然後 **[!UICONTROL 憑據]**。 有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請閱讀 [憑據指南](../ui/credentials.md)。

![Experience Platform查詢憑據面板，其中突出顯示了憑據。](../images/clients/power-bi/query-service-credentials-page.png)

對於 **[!DNL Server]** 在Power BI中，輸入在「查詢服務身份證明」部分中找到的主機的值。 對於生產，添加埠 `:80` 到主機字串的末尾。 例如 `made-up.platform-query.adobe.io:80`。

的 **[!DNL Database]** 欄位可以是「all」或資料集表名。 例如 `prod:all`。

>[!IMPORTANT]
>
>第三方BI工具中的嵌套資料結構可以被平展，以提高其可用性並減少檢索、分析、轉換和報告資料所需的工作量。 請參閱[`FLATTEN` 特徵](../best-practices/flatten-nested-data.md) 有關如何在連接到資料庫時激活此設定的說明。

![Power BI儀表板，其中突出顯示了伺服器和資料庫輸入欄位。](../images/clients/power-bi/postgresql-database-dialog.png)

### 資料連接模式

接下來，您可以 **[!DNL Data Connectivity mode]**。 選擇 **[!DNL Import]** 後跟 **[!DNL OK]** 顯示所有可用表的清單，或選擇 **[!DNL DirectQuery]** 直接查詢資料源，而不直接將資料導入或複製到Power BI。

瞭解有關 **[!DNL Import]** 模式，請閱讀上 [導入表](#import)。 瞭解有關 **[!DNL DirectQuery]** 模式，請閱讀上 [在不導入資料的情況下查詢資料集](#direct-query)。

選擇 **[!DNL OK]** 確認資料庫詳細資訊後。

![](../images/clients/power-bi/connectivity-mode.png)

### 驗證

出現詢問您的用戶名、密碼和應用程式設定的提示。 此情況下的用戶名是您的組織ID，密碼是您的身份驗證令牌。 在「查詢服務身份證明」頁上可以找到這兩個身份證明。

填寫這些詳細資訊，然後選擇 **[!DNL Connect]** 繼續下一步。

![](../images/clients/power-bi/import-mode.png)

## 導入表 {#import}

通過選擇 **[!DNL Import]** [!DNL Data Connectivity mode]，將導入完整資料集，以便您按原樣使用Power BI案頭應用程式中的選定表和列。

>[!IMPORTANT]
>
>要查看自初始導入以來發生的資料更改，必須通過再次導入完整資料集來刷新Power BI中的資料。

要導入表，請輸入伺服器和資料庫詳細資訊 [如上所述](#connect-power-bi) 的 **[!DNL Import]** [!DNL Data Connectivity mode]，後跟 **[!DNL OK]**。 將顯示一個對話框，其中顯示所有可用表的清單。 選擇要預覽的表，然後 **[!DNL Load]** 將資料集放入Power BI。

![](../images/clients/power-bi/preview-table.png)

現在，表已導入Power BI。

![](../images/clients/power-bi/import-table.png)

### 使用自定義SQL導入表

Power BI和其他第三方工具（如Tableau）當前不允許用戶導入嵌套對象，如平台中的XDM對象。 要解決此問題，Power BI允許您使用自定義SQL訪問這些嵌套欄位並建立資料的拼合視圖。 Power BI將先前嵌套資料的此展平視圖作為普通表載入。

從PostgreSQL資料庫跨距中，選擇 **[!DNL Advanced options]** 在 **[!DNL SQL statement]** 的子菜單。 此自定義查詢應用於將JSON名稱值對拼合為表格格式。

![資料連接模式高級選項，用於建立自定義SQL陳述式。](../images/clients/power-bi/custom-sql-statement.png)

輸入自定義查詢後，選擇 **[!DNL OK]** 繼續連接資料庫。 查看 [認證](#authentication) 以獲取有關從此工作流部分連接資料庫的指導。

Power BI完成後，展平資料的預覽將作為表顯示在案頭儀表板中。 伺服器和資料庫名稱列在對話框頂部。 選擇 **[!DNL Load]** 完成導入過程。

![Power BI操控板中展平的導入表。](../images/clients/power-bi/imported-table-preview.png)

可視化效果現在可用於編輯和從Power BI案頭應用導出。

## 查詢資料集而不導入資料 {#direct-query}

的 **[!DNL DirectQuery]** [!DNL Data Connectivity mode] 直接查詢資料源，而不將資料導入或複製到Power BI案頭。 使用此連接模式，可以通過UI使用當前資料刷新所有可視化效果。 但是，生成或刷新可視化所需的時間會因基礎資料源的效能而異。

使用此 [!DNL Data Connectivity mode]，選擇 **[!DNL DirectQuery]** 切換 **[!DNL Advanced options]** 在 **[!DNL SQL statement]** 的子菜單。 確保 **[!DNL Include relationship columns]** 的子菜單。 完成查詢後，選擇 **[!DNL OK]** 繼續。

![](../images/clients/power-bi/direct-query-mode.png)

將顯示查詢的預覽。 選擇 **[!DNL Load]** 的子菜單。

![](../images/clients/power-bi/preview-direct-query.png)

## 後續步驟

通過閱讀此文檔，您現在應該瞭解如何連接到Power BI案頭應用以及可用的不同資料連接模式。 有關如何編寫和運行查詢的詳細資訊，請參閱 [查詢執行指南](../best-practices/writing-queries.md)。
