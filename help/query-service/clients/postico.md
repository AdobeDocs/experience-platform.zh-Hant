---
keywords: Experience Platform; home；熱門主題；查詢服務；查詢服務；postico; Postico；連接到查詢服務；
solution: Experience Platform
title: 將Postico連接至查詢服務
topic-legacy: connect
description: 本文檔包含用於安裝備份客戶端Postico forAdobe Experience Platform查詢服務的連結。
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# 將[!DNL Postico]連接到查詢服務(Mac)

本文檔介紹將[!DNL Postico]與Adobe Experience Platform[!DNL Query Service]連接的步驟。

>[!NOTE]
>
> 本指南假定您已經擁有[!DNL Postico]的訪問權限，並熟悉如何導航其介面。 有關[!DNL Postico]的更多資訊，請參閱[official [!DNL Postico] 文檔](https://eggerapps.at/postico/docs)。
> 
> 此外，[!DNL Postico]僅&#x200B;**適用於macOS裝置。**

要將[!DNL Postico]連接到查詢服務，請開啟[!DNL Postico]並選擇&#x200B;**[!DNL New Favorite]**。

![](../images/clients/postico/open-postico.png)

您現在可以輸入值以連接Adobe Experience Platform。

有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請訪問Platform](https://platform.adobe.com/query/configuration)上的[ credentials頁。 若要尋找您的認證，請登入[!DNL Platform]，然後選取&#x200B;**[!UICONTROL Queries]**，後面接著&#x200B;**[!UICONTROL Credentials]**。

插入憑據後，選擇&#x200B;**[!DNL Connect]**&#x200B;以連接查詢服務。

![](../images/clients/postico/authentication-details.png)

連接到平台後，您將能夠看到先前與查詢服務建立的所有關係的清單。

![](../images/clients/postico/show-queries.png)

## 建立SQL陳述式

要建立新的SQL查詢，請選擇並開啟「SQL查詢」。

![](../images/clients/postico/create-query.png)

隨即出現一個框，您可以在此鍵入要執行的查詢。 完成後，選擇&#x200B;**[!DNL Execute Statement]**&#x200B;以運行查詢。

![](../images/clients/postico/run-statement.png)

此時會出現一個表格，顯示已完成查詢運行的結果。

![](../images/clients/postico/query-results.png)

## 後續步驟

現在您已連接[!DNL Query Service]，您可以使用[!DNL Postico]來編寫查詢。 有關如何寫入和運行查詢的詳細資訊，請閱讀[運行查詢指南](../best-practices/writing-queries.md)。
