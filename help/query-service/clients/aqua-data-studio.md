---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Aqua Data Studio連接
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# 連接 [!DNL Aqua Data Studio]

本檔案將逐步說明如何連接 [!DNL Aqua Data Studio] Adobe Experience Platform [!DNL Query Service]。

安裝後 [!DNL Aqua Data Studio]，您必須先註冊伺服器。 在主菜單中，按一下「服 **[!UICONTROL 務器]**」 ，然後按一下「 **[!UICONTROL 註冊伺服器」]**。

![](../images/clients/aqua-data-studio/register-server.png)

將出 *[!UICONTROL 現「註冊伺服器]* 」對話框。 在「常 *[!UICONTROL 規]* 」頁籤下，從左側的列 **[!UICONTROL 表中選擇「PostgreSQL]** 」。 在出現的對話方塊中，提供伺服器設定的下列詳細資訊。

- **[!UICONTROL 名稱]**: 連線的名稱。
- **[!UICONTROL 登入名稱和密碼]**: 將使用的登錄憑據。 用戶名的形式為 `ORG_ID@AdobeOrg`。
- **[!UICONTROL 主機和埠]**: 主機端點及其埠 [!DNL Query Service]。
- **[!UICONTROL 資料庫]:**將使用的資料庫。

>[!NOTE]
>
>有關查找登錄憑據、主機、埠和資料庫名稱的詳細資訊，請訪問平台 [上的憑據頁](https://platform.adobe.com/query/configuration)。 若要尋找您的認證，請登入，按一 [!DNL Platform]下「查 **[!UICONTROL 詢]**」，然後按一 **[!UICONTROL 下「認證]**」。

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

選擇「驅動 **[!UICONTROL 程式]** 」頁籤。 在「參 *[!UICONTROL 數]*」(Parameters)下，將值設定為 `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

在輸入連線詳細資訊後，按一下「 **[!UICONTROL 測試連線]** 」以確保憑證正常運作。 如果連線成功，請按一下「 **[!UICONTROL 儲存]** 」以註冊您的伺服器。 成功註冊後，連線會出 *現在「儀表板* 」上，確認您現在可以連線至伺服器並檢視其架構物件。

## 後續步驟

現在，您已連接到 [!DNL Query Service]，您可以使用中的 *[!UICONTROL Query Analyzer]* , [!DNL Aqua Data Studio] 執行和編輯SQL陳述式。 有關如何編寫和運行查詢的詳細資訊，請閱讀運行查 [詢指南](../creating-queries/creating-queries.md)。