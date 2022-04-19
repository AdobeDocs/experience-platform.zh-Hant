---
keywords: Experience Platform；主題；熱門主題；查詢服務；查詢服務；瀏覽器；瀏覽器；連接到查詢服務；
solution: Experience Platform
title: 將查找程式連接到查詢服務
topic-legacy: connect
description: 本文檔介紹了將Looker與Adobe Experience Platform查詢服務連接的步驟。
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: ad3e1b0de6dd3b82cc82f0dc3d0f36b12cd3899e
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# 連接 [!DNL Looker] 查詢服務

本文檔介紹了連接 [!DNL Looker] 與Adobe Experience Platform [!DNL Query Service]。

>[!NOTE]
>
> 本指南假定您已具有訪問 [!DNL Looker] 並熟悉如何導航其介面。 有關 [!DNL Looker] 在 [官 [!DNL Looker] 文檔](https://docs.looker.com/)。

登錄後 [!DNL Looker]選中 **[!DNL Admin]**，後跟 **[!DNL Connections]**。

![](../images/clients/looker/click-admin-connections.png)

在此頁上，選擇 **[!DNL New Connection]**。

![](../images/clients/looker/click-new-connection.png)

在此處，您可以填寫連接設定的詳細資訊。

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** 連接的名稱。
- **[!DNL Dialect]:** 用於SQL資料庫的方言。 [!DNL Query Service] 使用 **[!DNL PostgreSQL]**。
- **[!DNL Host and Port]:** 用於的主機終結點及其埠 [!DNL Query Service]。
- **[!DNL Database]:** 將使用的資料庫。
- **[!DNL Username and Password]:** 將使用的登錄憑據。 用戶名將以 `ORG_ID@AdobeOrg`。
- **SSL**:啟用SSL以確保跨網路的安全連接。

>[!IMPORTANT]
>
>查看 [[!DNL Query Service] SSL文檔](./ssl-modes.md) 瞭解對與Adobe Experience Platform查詢服務的第三方連接的SSL支援，以及如何使用 `verify-full` SSL模式。

有關查找主機和埠、資料庫名稱和登錄憑據的詳細資訊，請閱讀 [憑據指南](../ui/credentials.md)。 要查找憑據，請登錄到 [!DNL Platform]，然後選擇 **[!UICONTROL 查詢]**，後跟 **[!UICONTROL 憑據]**。

輸入連接詳細資訊後，選擇 **[!DNL Test These Settings]** 以確保您的憑據正常工作。 如果他們這樣做，則下面將顯示一條消息，指示您可以連接。 如果連接確實成功，請選擇 **[!DNL Add Connection]** 建立連接。

![](../images/clients/looker/click-test-connection.png)

## 後續步驟

既然你已經和 [!DNL Query Service]，您可以使用 [!DNL Looker] 來編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢指南](../best-practices/writing-queries.md)。
