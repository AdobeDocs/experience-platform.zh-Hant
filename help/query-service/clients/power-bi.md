---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；Power BI；電源；連接到查詢服務；
solution: Experience Platform
title: 將Power BI連接到查詢服務
description: 本文檔將介紹與Adobe Experience Platform查詢服務連接Power BI的步驟。
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '1067'
ht-degree: 1%

---

# 連接 [!DNL Power BI] 查詢服務

本文檔介紹了連接 [!DNL Power BI] 具有Adobe Experience Platform查詢服務的台式機。

## 快速入門

本指南要求您已具有訪問 [!DNL Power BI] 案頭應用，並熟悉如何瀏覽其介面。 下載 [!DNL Power BI] 案頭或有關詳細資訊，請參閱 [官 [!DNL Power BI] 文檔](https://docs.microsoft.com/zh-tw/power-bi/)。

>[!IMPORTANT]
>
> 的 [!DNL Power BI] 案頭應用程式 **僅** 在Windows設備上可用。

獲取連接所需的憑據 [!DNL Power BI] 要Experience Platform，您必須有權訪問平台UI中的「查詢」工作區。 如果您當前沒有訪問查詢工作區的權限，請與組織管理員聯繫。

安裝後 [!DNL Power BI]，您需要安裝 `Npgsql`，用於PostgreSQL的.NET驅動程式包。 有關Npgsql的詳細資訊，請參見 [Npgsql文檔](https://www.npgsql.org/doc/index.html)。

>[!IMPORTANT]
>
>您必須下載v4.0.10或更低版本，因為較新版本會導致錯誤。

在「」下[!DNL Npgsql GAC Installation]&quot;在自定義設定螢幕上，選擇 **[!DNL Will be installed on local hard drive]**。

要確保Npgsql已正確安裝，請在繼續執行後續步驟之前重新啟動電腦。

## 連接 [!DNL Power BI] 查詢服務 {#connect-power-bi}

連接 [!DNL Power BI] 到查詢服務，開啟 [!DNL Power BI] 選擇 **[!DNL Get Data]** 的子菜單。 下一步，輸入&quot;[!DNL PostgreSQL]」，以縮小資料源清單的範圍。 從顯示的結果中，選擇 **[!DNL PostgreSQL database]**，後跟 **[!DNL Connect]**。

的 [!DNL PostgreSQL] 資料庫對話框，請求伺服器和資料庫的值。 有關如何 [從Power Query Desktop連接到PostgreSQL資料庫](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) 可以在官員那裡找到 [!DNL PowerBI] 文檔。

這些必需值取自您的Adobe Experience Platform憑據。 要查找憑據，請登錄到平台UI並選擇 **[!UICONTROL 查詢]** 從左導航，然後 **[!UICONTROL 憑據]**。 有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請閱讀 [憑據指南](../ui/credentials.md)。

![「Experience Platform查詢」工作區中突出顯示了「憑據」頁籤和「過期」憑據。](../images/clients/power-bi/query-service-credentials-page.png)

在 **[!DNL Server]** 的 [!DNL PostgreSQL database] 對話框，輸入在查詢服務中找到的主機的值 [!UICONTROL 憑據] 的子菜單。 對於生產，添加埠 `:80` 到主機字串的末尾。 例如 `made-up.platform-query.adobe.io:80`。

的 **[!DNL Database]** 欄位可以是「all」或資料集表名。 例如 `prod:all`。

>[!IMPORTANT]
>
>第三方BI工具中的嵌套資料結構可以被平展，以提高其可用性並減少檢索、分析、轉換和報告資料所需的工作量。 請參閱[`FLATTEN` 特徵](../essential-concepts/flatten-nested-data.md) 有關如何在連接到資料庫時激活此設定的說明。

### 資料連接模式 {#data-connectivity-mode}

接下來，您可以 **[!DNL Data Connectivity mode]**。 在 [!DNL PostgreSQL database] 對話框，選擇 **[!DNL Import]** 後跟 **[!DNL OK]** 顯示所有可用表的清單，或選擇 **[!DNL DirectQuery]** 直接查詢資料源，而不直接將資料導入或複製到 [!DNL Power BI]。

瞭解有關 **[!DNL Import]** 模式，請閱讀上 [導入表](#import)。 瞭解有關 **[!DNL DirectQuery]** 模式，請閱讀上 [在不導入資料的情況下查詢資料集](#direct-query)。

選擇 **[!DNL OK]** 確認資料庫詳細資訊後。

### 驗證 {#authentication}

確認資料連接模式後，將出現提示，詢問您的用戶名、密碼和應用程式設定。 此情況下的用戶名是您的組織ID，密碼是您的身份驗證令牌。 在「查詢服務身份證明」頁上可以找到這兩個身份證明。

填寫這些詳細資訊，然後選擇 **[!DNL Connect]** 繼續下一步。

## 導入表 {#import}

通過選擇 **[!DNL Import]** [!DNL Data Connectivity mode]，將導入完整資料集，以便您使用 [!DNL Power BI] 案頭應用程式原樣。

>[!IMPORTANT]
>
>要查看自初始導入以來發生的資料更改，必須刷新 [!DNL Power BI] 重新導入完整資料集。

要導入表，請輸入伺服器和資料庫詳細資訊 [如上所述](#connect-power-bi) 的 **[!DNL Import]** [!DNL Data Connectivity mode]，後跟 **[!DNL OK]**。 的 [!DNL Navigator] 對話框，顯示所有可用表的清單。 選擇要預覽的表，然後 **[!DNL Load]** 將資料集放入Power BI。 表現在已導入 [!DNL Power BI]。

[有關連接到PowerBi台式機中資料的一般資訊](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) 官方文檔中可找到app。

### 使用自定義SQL導入表

[!DNL Power BI] 和其他第三方工具 [!DNL Tableau] 當前不允許用戶導入嵌套對象，如平台中的XDM對象。 為了說明這一點， [!DNL Power BI] 允許您使用自定義SQL訪問這些嵌套欄位並建立資料的拼合視圖。 [!DNL Power BI] 然後將先前嵌套資料的此平展視圖作為普通表載入。

從 [!DNL PostgreSQL database] 對話框，選擇 **[!DNL Advanced options]** 在 **[!DNL SQL statement]** 的子菜單。 此自定義查詢應用於將JSON名稱值對拼合為表格格式。 官方檔案還提供了如何 [在高級選項中使用SQL陳述式連接PowerBI](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options)。

輸入自定義查詢後，選擇 **[!DNL OK]** 繼續連接資料庫。 查看 [認證](#authentication) 以獲取有關從此工作流部分連接資料庫的指導。

驗證完成後，將在 [!DNL Power BI] 案頭儀表板作為表。 伺服器和資料庫名稱列在對話框頂部。 選擇 **[!DNL Load]** 完成導入過程。

現在，可視化可用於編輯和從 [!DNL Power BI] 案頭應用。

## 查詢資料集而不導入資料 {#direct-query}

的 **[!DNL DirectQuery]** [!DNL Data Connectivity mode] 直接查詢資料源，而不將資料導入或複製到 [!DNL Power BI] 台式機。 使用此連接模式，可以通過UI使用當前資料刷新所有可視化效果。 但是，生成或刷新可視化所需的時間會因基礎資料源的效能而異。

有關 [使用 [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) 以及對它的全面討論 [連接選項、使用案例和限制](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) 可以在官員那裡找到 [!DNL PowerBI] 文檔。

使用此 [!DNL Data Connectivity mode]，選擇 **[!DNL DirectQuery]** 切換 **[!DNL Advanced options]** 在 **[!DNL SQL statement]** 的子菜單。 確保 **[!DNL Include relationship columns]** 的子菜單。 完成查詢後，選擇 **[!DNL OK]** 繼續。

將顯示查詢的預覽。 選擇 **[!DNL Load]** 的子菜單。

## 後續步驟

通過閱讀此文檔，您現在應瞭解如何連接到 [!DNL Power BI] 案頭應用和不同的資料連接模式可用。 有關如何編寫和運行查詢的詳細資訊，請參閱 [查詢執行指南](../best-practices/writing-queries.md)。
