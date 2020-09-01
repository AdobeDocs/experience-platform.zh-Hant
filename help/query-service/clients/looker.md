---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: 與Looker連接
topic: connect
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# 連接 [!DNL Looker]

若要連 [!DNL Looker] 接 [!DNL Query Service] Adobe Experience Platform，請遵循下列步驟：

登入後，按 [!DNL Looker]一下「管 **[!UICONTROL 理]**」，接著 **[!UICONTROL 按「連線」]**。

![](../images/clients/looker/click-admin-connections.png)

在此頁上，按一下「 **New Connection（新建連接）**」。

![](../images/clients/looker/click-new-connection.png)

從這裡，您可以填寫「連線設定」的詳細資訊。

![](../images/clients/looker/new-connection.png)

- **名稱：** 連線的名稱。
- **方言：** 用於SQL資料庫的方言。 [!DNL Query Service] 使用 **[!DNL PostgreSQL]**&#x200B;者。
- **主機和埠：** 主機端點及其埠 [!DNL Query Service]。
- **資料庫：** 將使用的資料庫。
- **使用者名稱與密碼：** 將使用的登錄憑據。 用戶名的格式為 `ORG_ID@AdobeOrg`。

>[!NOTE]
>
>有關查找主機和埠、資料庫名和登錄憑據的詳細資訊，請訪問平台 [上的憑據頁](https://platform.adobe.com/query/configuration)。 若要尋找您的認證，請登入，按一 [!DNL Platform]下「查 **[!UICONTROL 詢]**」，然後按一 **[!UICONTROL 下「認證]**」。

輸入連線詳細資訊後，按一下「測 **[!UICONTROL 試這些設定」]** ，以確保憑證正常運作。 如果是，則會在下方顯示訊息，告知您可以連線。 如果您的連線確實成功，請按一下「 **[!UICONTROL 新增連線]** 」以建立連線。

![](../images/clients/looker/click-test-connection.png)

## 後續步驟

現在您已連線，您 [!DNL Query Service]可以使用來 [!DNL Looker] 編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀運行查 [詢指南](../creating-queries/creating-queries.md)。