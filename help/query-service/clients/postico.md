---
keywords: Experience Platform；首頁；熱門主題；查詢服務；貼文；貼文；連線至查詢服務；
solution: Experience Platform
title: 將Postico連接到Query Service
topic-legacy: connect
description: 本檔案包含安裝Adobe Experience Platform Query Service備份用戶端Postico的連結。
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 將[!DNL Postico]連接到查詢服務(Mac)

本檔案說明將[!DNL Postico]與Adobe Experience Platform [!DNL Query Service]連接的步驟。

>[!NOTE]
>
> 本指南假設您已擁有[!DNL Postico]的存取權，且熟悉如何導覽其介面。 有關[!DNL Postico]的更多資訊，請參閱[official [!DNL Postico] documentation](https://eggerapps.at/postico/docs)。
> 
> 此外，[!DNL Postico]僅&#x200B;**可在macOS裝置上使用。**

要將[!DNL Postico]連接到查詢服務，請開啟[!DNL Postico]並選擇&#x200B;**[!DNL New Favorite]**。

![](../images/clients/postico/open-postico.png)

您現在可以輸入值以連線至Adobe Experience Platform。

有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請參閱[憑據指南](../ui/credentials.md)。 要查找憑據，請登錄[!DNL Platform]，然後選擇&#x200B;**[!UICONTROL 查詢]**，後跟&#x200B;**[!UICONTROL 憑據]**。

插入憑據後，選擇&#x200B;**[!DNL Connect]**&#x200B;以與查詢服務連接。

![](../images/clients/postico/authentication-details.png)

連線至Platform後，您將會看到先前與Query Service建立的所有關係清單。

![](../images/clients/postico/show-queries.png)

## 建立SQL陳述式

要建立新的SQL查詢，請選擇並開啟「SQL查詢」。

![](../images/clients/postico/create-query.png)

隨即出現方塊，您可以在此處輸入要執行的查詢。 完成後，選擇&#x200B;**[!DNL Execute Statement]**&#x200B;以運行查詢。

![](../images/clients/postico/run-statement.png)

隨即出現表格，顯示已完成查詢運行的結果。

![](../images/clients/postico/query-results.png)

## 後續步驟

現在您已連接[!DNL Query Service]，可以使用[!DNL Postico]來編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀[運行查詢指南](../best-practices/writing-queries.md)。
