---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查找者；查找者；連接到查詢服務；
solution: Experience Platform
title: 將登錄程式連接到查詢服務
topic-legacy: connect
description: 本檔案會逐步說明連接Looker與Adobe Experience Platform Query Service的步驟。
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Connect [!DNL Looker] 查詢服務

本檔案涵蓋連接 [!DNL Looker] 搭配Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假設您已擁有 [!DNL Looker] 並熟悉如何導覽其介面。 有關 [!DNL Looker] 可在 [官方 [!DNL Looker] 檔案](https://docs.looker.com/).

登入後 [!DNL Looker]，選取 **[!DNL Admin]**，後跟 **[!DNL Connections]**.

![此 [!DNL Looker] 從「管理」下拉式功能表中強調顯示「連線」的控制面板。](../images/clients/looker/click-admin-connections.png)

在此頁面上，選取 **[!DNL New Connection]**.

![「具有新連接的連接」工作區突出顯示。](../images/clients/looker/click-new-connection.png)

從這裡，您可以填寫連線設定的詳細資訊。

![新連接的「連接設定」頁。](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** 連線的名稱。
- **[!DNL Dialect]:** 用於SQL資料庫的方言。 [!DNL Query Service] uses **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** 的主機端點及其埠 [!DNL Query Service].
- **[!DNL Database]:** 將使用的資料庫。
- **[!DNL Username and Password]:** 將使用的登入憑證。 使用者名稱將以 `ORG_ID@AdobeOrg`.
- **SSL**:啟用SSL以確保跨網路的安全連接。

>[!IMPORTANT]
>
>請參閱 [[!DNL Query Service] SSL檔案](./ssl-modes.md) 了解協力廠商連線至Adobe Experience Platform Query Service的SSL支援，以及如何使用 `verify-full` SSL模式。

有關查找主機和埠、資料庫名和登錄憑據的詳細資訊，請閱讀 [認證指南](../ui/credentials.md). 若要尋找憑證，請登入 [!DNL Platform]，然後選取 **[!UICONTROL 查詢]**，後跟 **[!UICONTROL 憑證]**.

輸入連線詳細資訊後，請選取 **[!DNL Test These Settings]** 以確保憑證正常運作。 如果有，下方會顯示訊息，指出您可以連線。 如果您的連線確實成功，請選取 **[!DNL Add Connection]** 來建立連線。

![「New Connection with Test these settings（通過測試新連接）」的「Connections（連接）」設定頁突出顯示。](../images/clients/looker/click-test-connection.png)

## 後續步驟

既然你已經和 [!DNL Query Service]，您可以使用 [!DNL Looker] 來寫入查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢指南](../best-practices/writing-queries.md).
