---
keywords: Experience Platform; home；熱門主題；查詢服務；查詢服務； Aqua Data Studio; Aqua data studio；連接查詢服務；
solution: Experience Platform
title: 使用Aqua Data Studio連接
topic: connect
description: 本檔案將逐步說明如何將Aqua Data Studio與Adobe Experience Platform Query Service連結。
translation-type: tm+mt
source-git-commit: eac93f3465fa6ce4af7a6aa783cf5f8fb4ac9b9b
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---


# [!DNL Aqua Data Studio]

本檔案涵蓋連接[!DNL Aqua Data Studio]與Adobe Experience Platform [!DNL Query Service]的步驟。

>[!NOTE]
>
> 本指南假定您已經擁有[!DNL Aqua Data Studio]的訪問權限，並熟悉如何導航其介面。 有關[!DNL Aqua Data Studio]的更多資訊，請參閱[official [!DNL Aqua Data Studio] 文檔](https://www.aquaclusters.com/app/home/project/public/aquadatastudio/wikibook/Documentation21.1/page/0/Aqua-Data-Studio-21-1)。

## 連接[!DNL Aqua Data Studio]平台

安裝[!DNL Aqua Data Studio]後，必須先註冊伺服器。 從主菜單中，選擇&#x200B;**[!DNL Server]** ，然後選擇&#x200B;**[!DNL Register Server]**。

![](../images/clients/aqua-data-studio/register-server.png)

出現&#x200B;**[!DNL Register Server]**&#x200B;對話框。 在&#x200B;**[!DNL General]**&#x200B;標籤下，從左側的清單中選擇&#x200B;**[!DNL PostgreSQL]**。 在出現的對話方塊中，提供伺服器設定的下列詳細資訊。

- **[!DNL Name]**:連線的名稱。
- **[!DNL Login Name and Password]**:將使用的登錄憑據。用戶名的形式為`ORG_ID@AdobeOrg`。
- **[!DNL Host and Port]**:主機端點及其埠 [!DNL Query Service]。必須使用埠80連接[!DNL Query Service]。
- **[!DNL Database]:** 將使用的資料庫。

>[!NOTE]
>
>有關查找登錄憑據、主機、埠和資料庫名稱的詳細資訊，請訪問Platform](https://platform.adobe.com/query/configuration)上的[憑據頁。 要查找憑據，請登錄到[!DNL Platform]，然後選擇&#x200B;**[!UICONTROL 查詢]**，然後選擇&#x200B;**[!UICONTROL 憑據]**。

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

選取 **[!DNL Driver]** 索引標籤。在&#x200B;**[!DNL Parameters]**&#x200B;下，將值設定為`?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

在輸入連線詳細資訊後，請選取&#x200B;**[!DNL Test Connection]**&#x200B;以確保憑證正常運作。 如果連接成功，請選擇&#x200B;**[!DNL Save]**&#x200B;註冊伺服器。 成功註冊後，連接會顯示在儀表板上，確認您現在可以連接到伺服器並查看其方案對象。

## 後續步驟

現在您已連接到[!DNL Query Service]，您可以使用[!DNL Aqua Data Studio]中的&#x200B;**[!DNL Query Analyzer]**&#x200B;來執行和編輯SQL陳述式。 有關如何寫入和運行查詢的詳細資訊，請閱讀[運行查詢指南](../best-practices/writing-queries.md)。