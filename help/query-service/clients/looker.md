---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: 與Looker連接
topic: connect
description: 本檔案將逐步說明如何將Looker與Adobe Experience Platform Query Service連接。
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 連接[!DNL Looker]

若要在Adobe Experience Platform上將[!DNL Looker]與[!DNL Query Service]連線，請遵循下列步驟：

登入[!DNL Looker]後，按一下&#x200B;**[!UICONTROL Admin]**，然後按一下&#x200B;**[!UICONTROL Connections]**。

![](../images/clients/looker/click-admin-connections.png)

在此頁上，按一下&#x200B;**新建連接**。

![](../images/clients/looker/click-new-connection.png)

從這裡，您可以填寫「連線設定」的詳細資訊。

![](../images/clients/looker/new-connection.png)

- **名稱：** 連線的名稱。
- **方言：** 用於SQL資料庫的方言。[!DNL Query Service] 使用 **[!DNL PostgreSQL]**&#x200B;者。
- **主機和埠：** 主機端點及其埠 [!DNL Query Service]。
- **資料庫：** 將使用的資料庫。
- **使用者名稱和** 密碼：將使用的登入憑證。用戶名的格式為`ORG_ID@AdobeOrg`。

>[!NOTE]
>
>有關查找主機和埠、資料庫名和登錄憑據的詳細資訊，請訪問Platform](https://platform.adobe.com/query/configuration)上的[憑據頁。 要查找憑據，請登錄到[!DNL Platform] ，按一下&#x200B;**[!UICONTROL 查詢]** ，然後按一下&#x200B;**[!UICONTROL 憑據]**。

在輸入連線詳細資訊後，按一下「測試這些設定」]**，以確保憑證正常運作。**[!UICONTROL &#x200B;如果是，則會在下方顯示訊息，告知您可以連線。 如果連接確實成功，請按一下&#x200B;**[!UICONTROL 添加連接]**&#x200B;以建立連接。

![](../images/clients/looker/click-test-connection.png)

## 後續步驟

現在您已連接[!DNL Query Service]，您可以使用[!DNL Looker]來編寫查詢。 有關如何寫入和運行查詢的詳細資訊，請閱讀[運行查詢指南](../best-practices/writing-queries.md)。