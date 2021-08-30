---
keywords: Experience Platform；首頁；熱門主題；tableau;Tableau；查詢服務；查詢服務；連線至查詢服務；
solution: Experience Platform
title: 將 Tableau 連接至查詢服務
topic-legacy: connect
description: 本檔案會逐步說明將Tableau與Adobe Experience Platform Query Service連線的步驟。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 3%

---

# 將[!DNL Tableau]連接到查詢服務

本檔案說明連接Tableau與Adobe Experience Platform [!DNL Query Service]的步驟。

>[!NOTE]
>
> 本指南假設您已擁有[!DNL Tableau]的存取權，且熟悉如何導覽其介面。 有關[!DNL Tableau]的更多資訊，請參閱[official [!DNL Tableau] documentation](https://help.tableau.com/current/pro/desktop/en-us/default.htm)。

要將[!DNL Tableau]連接到[!DNL Query Service]，請開啟[!DNL Tableau]，並在&#x200B;**[!DNL To a Server]**&#x200B;部分中選擇&#x200B;**[!DNL More]**，然後選擇&#x200B;**[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

您現在可以輸入值以連線至Adobe Experience Platform。 有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請參閱[憑據指南](../ui/credentials.md)。 要查找憑據，請登錄[!DNL Platform]，然後選擇&#x200B;**[!UICONTROL 查詢]**，後跟&#x200B;**[!UICONTROL 憑據]**。

在嘗試連接之前，請確保已選中&#x200B;**[!UICONTROL SSL必需]**&#x200B;框。

填寫所有憑據後，請選擇&#x200B;**[!DNL Sign In]**&#x200B;以繼續。

![](../images/clients/tableau/sign-in.png)

您現在已連線Adobe Experience Platform，側面會顯示表格清單。

![](../images/clients/tableau/connected.png)

## 後續步驟

現在您已連接[!DNL Query Service]，可以使用[!DNL Tableau]來編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀[運行查詢](../best-practices/writing-queries.md)的指南。
