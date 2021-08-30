---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查找者；查找者；連接到查詢服務；
solution: Experience Platform
title: 將登錄程式連接到查詢服務
topic-legacy: connect
description: 本檔案會逐步說明連接Looker與Adobe Experience Platform Query Service的步驟。
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 將[!DNL Looker]連接到查詢服務

本檔案說明將[!DNL Looker]與Adobe Experience Platform [!DNL Query Service]連接的步驟。

>[!NOTE]
>
> 本指南假設您已擁有[!DNL Looker]的存取權，且熟悉如何導覽其介面。 有關[!DNL Looker]的更多資訊，請參閱[official [!DNL Looker] documentation](https://docs.looker.com/)。

登入[!DNL Looker]後，選取&#x200B;**[!DNL Admin]**，後接&#x200B;**[!DNL Connections]**。

![](../images/clients/looker/click-admin-connections.png)

在此頁上，選擇&#x200B;**[!DNL New Connection]**。

![](../images/clients/looker/click-new-connection.png)

從這裡，您可以填寫連線設定的詳細資訊。

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** 連線的名稱。
- **[!DNL Dialect]:** 用於SQL資料庫的方言。[!DNL Query Service] 使用 **[!DNL PostgreSQL]**。
- **[!DNL Host and Port]:** 的主機端點及其連接 [!DNL Query Service]埠。
- **[!DNL Database]:** 將使用的資料庫。
- **[!DNL Username and Password]:** 將使用的登入憑證。用戶名將以`ORG_ID@AdobeOrg`的形式顯示。

>[!NOTE]
>
>有關查找主機和埠、資料庫名和登錄憑據的詳細資訊，請參閱[憑據指南](../ui/credentials.md)。 要查找憑據，請登錄[!DNL Platform]，然後選擇&#x200B;**[!UICONTROL 查詢]**，後跟&#x200B;**[!UICONTROL 憑據]**。

輸入連接詳細資訊後，選擇&#x200B;**[!DNL Test These Settings]**&#x200B;以確保憑據正常工作。 如果有，下方會顯示訊息，指出您可以連線。 如果連接確實成功，請選擇&#x200B;**[!DNL Add Connection]**&#x200B;建立連接。

![](../images/clients/looker/click-test-connection.png)

## 後續步驟

現在您已連接[!DNL Query Service]，可以使用[!DNL Looker]來編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀[運行查詢指南](../best-practices/writing-queries.md)。
