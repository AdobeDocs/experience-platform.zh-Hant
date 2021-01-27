---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: 使用Aqua Data Studio連接
topic: connect
description: 本檔案將逐步說明如何將Aqua Data Studio與Adobe Experience Platform Query Service連結。
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# 連接[!DNL Aqua Data Studio]

本檔案將逐步說明如何連接[!DNL Aqua Data Studio]與Adobe Experience Platform [!DNL Query Service]。

安裝[!DNL Aqua Data Studio]後，必須先註冊伺服器。 在主菜單中，按一下&#x200B;**[!UICONTROL 伺服器]** ，然後按一下&#x200B;**[!UICONTROL 註冊伺服器]**。

![](../images/clients/aqua-data-studio/register-server.png)

出現&#x200B;**[!UICONTROL 註冊伺服器]**&#x200B;對話框。 在&#x200B;**[!UICONTROL General]**&#x200B;標籤下，從左側的清單中選擇&#x200B;**[!UICONTROL PostgreSQL]**。 在出現的對話方塊中，提供伺服器設定的下列詳細資訊。

- **[!UICONTROL 名稱]**:連線的名稱。
- **[!UICONTROL 登入名稱和密碼]**:將使用的登錄憑據。用戶名的形式為`ORG_ID@AdobeOrg`。
- **[!UICONTROL 主機和埠]**:主機端點及其埠 [!DNL Query Service]。必須使用埠80連接[!DNL Query Service]。
- **[!UICONTROL 資料]庫：** 將使用的資料庫。

>[!NOTE]
>
>有關查找登錄憑據、主機、埠和資料庫名稱的詳細資訊，請訪問Platform](https://platform.adobe.com/query/configuration)上的[憑據頁。 要查找憑據，請登錄到[!DNL Platform] ，按一下&#x200B;**[!UICONTROL 查詢]** ，然後按一下&#x200B;**[!UICONTROL 憑據]**。

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

選擇&#x200B;**[!UICONTROL 驅動程式]**&#x200B;頁籤。 在&#x200B;**[!UICONTROL Parameters]**&#x200B;下，將值設定為`?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

在輸入連線詳細資訊後，按一下「測試連線」**[!UICONTROL ，以確保憑證正常運作。]**&#x200B;如果連接成功，請按一下&#x200B;**[!UICONTROL 保存]**&#x200B;註冊伺服器。 成功註冊後，連線會出現在&#x200B;**Dashboard**&#x200B;中，確認您現在可以連線至伺服器並檢視其架構物件。

## 後續步驟

現在，您已連接到[!DNL Query Service]，可以使用[!DNL Aqua Data Studio]中的&#x200B;**[!UICONTROL 查詢分析器]**&#x200B;來執行和編輯SQL陳述式。 有關如何寫入和運行查詢的詳細資訊，請閱讀[運行查詢指南](../best-practices/writing-queries.md)。