---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Aqua Data Studio連接
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# 使用Aqua Data Studio連接

本檔案將逐步說明如何將Aqua Data Studio與Adobe Experience Platform Query Service連結。

安裝Aqua Data Studio後，您必須先註冊伺服器。 在主菜單中，按一下「服 **務器**」 ，然後按一下「 **註冊伺服器」**。

![](../images/clients/aqua-data-studio/register-server.png)

將出 *現「註冊伺服器* 」對話框。 在「常 *規* 」頁籤下，從左側的列 **表中選擇「PostgreSQL** 」。 在出現的對話方塊中，提供伺服器設定的下列詳細資訊。

- **名稱**: 連線的名稱。
- **登入名稱和密碼**: 將使用的登錄憑據。 用戶名的形式為 `ORG_ID@AdobeOrg`。
- **主機和埠**: 查詢服務的主機端點及其埠。
- **資料庫：** 將使用的資料庫。

>[!NOTE]
>
>有關查找登錄憑據、主機、埠和資料庫名稱的詳細資訊，請訪問平台 [上的憑據頁](https://platform.adobe.com/query/configuration)。 若要尋找您的認證，請登入「平台」，按一下「 **查詢**」，然後按一 **下「認證」**。

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

選擇「驅動 **程式** 」頁籤。 在「參 *數*」(Parameters)下，將值設定為 `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

在輸入連線詳細資訊後，按一下「 **測試連線** 」以確保憑證正常運作。 如果連線成功，請按一下「 **儲存** 」以註冊您的伺服器。 成功註冊後，連線會出 *現在「儀表板* 」上，確認您現在可以連線至伺服器並檢視其架構物件。

## 後續步驟

現在您已連接到Query Service，您可以使用Aqua Data Studio中的 *Query Analyzer* ，來執行和編輯SQL陳述式。 有關如何編寫和運行查詢的詳細資訊，請閱讀運行查 [詢指南](../creating-queries/creating-queries.md)。