---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 與Looker連接
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 與Looker連接

若要在Adobe Experience Platform上將Looker與Adobe Query Service連線，請遵循下列步驟：

登入Looker後，按一下「管 **理**」，接著按 **下「連線」**。

![](../images/clients/looker/click-admin-connections.png)

在此頁上，按一下「 **New Connection（新建連接）**」。

![](../images/clients/looker/click-new-connection.png)

從這裡，您可以填寫「連線設定」的詳細資訊。

![](../images/clients/looker/new-connection.png)

- **名稱：** 連線的名稱。
- **方言：** 用於SQL資料庫的方言。 查詢服務使 **用PostgreSQL**。
- **主機和埠：** 查詢服務的主機端點及其埠。
- **資料庫：** 將使用的資料庫。
- **使用者名稱與密碼：** 將使用的登錄憑據。 用戶名的格式為 `ORG_ID@AdobeOrg`。

>[!NOTE]
>
>有關查找主機和埠、資料庫名和登錄憑據的詳細資訊，請訪問平台 [上的憑據頁](https://platform.adobe.com/query/configuration)。 若要尋找您的認證，請登入「平台」，按一下「 **查詢**」，然後按一 **下「認證」**。

輸入連線詳細資訊後，按一下「測 **試這些設定」** ，以確保憑證正常運作。 如果是，則會在下方顯示訊息，告知您可以連線。 如果您的連線確實成功，請按一下「 **新增連線** 」以建立連線。

![](../images/clients/looker/click-test-connection.png)

## 後續步驟

現在您已連接Query Service，可以使用Looker來編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀運行查 [詢指南](../creating-queries/creating-queries.md)。