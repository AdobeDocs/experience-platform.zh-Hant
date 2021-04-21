---
keywords: Experience Platform; home；熱門主題；查詢服務；查詢服務； Looker;looker；連接到查詢服務；
solution: Experience Platform
title: 將Looker連接到查詢服務
topic-legacy: connect
description: 本檔案將逐步說明如何將Looker與Adobe Experience Platform查詢服務連接。
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 將[!DNL Looker]連接到查詢服務

本文檔介紹將[!DNL Looker]與Adobe Experience Platform[!DNL Query Service]連接的步驟。

>[!NOTE]
>
> 本指南假定您已經擁有[!DNL Looker]的訪問權限，並熟悉如何導航其介面。 有關[!DNL Looker]的更多資訊，請參閱[official [!DNL Looker] 文檔](https://docs.looker.com/)。

登入[!DNL Looker]後，選擇&#x200B;**[!DNL Admin]**，然後選擇&#x200B;**[!DNL Connections]**。

![](../images/clients/looker/click-admin-connections.png)

在此頁上，選擇&#x200B;**[!DNL New Connection]**。

![](../images/clients/looker/click-new-connection.png)

從這裡，您可以填寫連線設定的詳細資訊。

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** 連線的名稱。
- **[!DNL Dialect]:** 用於SQL資料庫的方言。[!DNL Query Service] 使用 **[!DNL PostgreSQL]**&#x200B;者。
- **[!DNL Host and Port]:** 主機端點及其埠 [!DNL Query Service]。
- **[!DNL Database]:** 將使用的資料庫。
- **[!DNL Username and Password]:** 將使用的登錄憑據。用戶名的格式為`ORG_ID@AdobeOrg`。

>[!NOTE]
>
>有關查找主機和埠、資料庫名和登錄憑據的詳細資訊，請訪問Platform](https://platform.adobe.com/query/configuration)上的[憑據頁。 若要尋找您的認證，請登入[!DNL Platform]，然後選取&#x200B;**[!UICONTROL Queries]**，後面接著&#x200B;**[!UICONTROL Credentials]**。

在輸入連線詳細資訊後，請選取&#x200B;**[!DNL Test These Settings]**&#x200B;以確保憑證正常運作。 如果有，則會在下方顯示一則訊息，指出您可以連線。 如果連接確實成功，請選擇&#x200B;**[!DNL Add Connection]**&#x200B;以建立連接。

![](../images/clients/looker/click-test-connection.png)

## 後續步驟

現在您已連接[!DNL Query Service]，您可以使用[!DNL Looker]來編寫查詢。 有關如何寫入和運行查詢的詳細資訊，請閱讀[運行查詢指南](../best-practices/writing-queries.md)。
