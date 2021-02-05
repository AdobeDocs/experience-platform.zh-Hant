---
keywords: Experience Platform;home;popular topics;tableau;Tableau；查詢服務；查詢服務；連接到查詢服務；
solution: Experience Platform
title: 將Tableau連接至查詢服務
topic: connect
description: 本檔案將逐步說明如何將Tableau與Adobe Experience Platform Query Service連接。
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---


# 將[!DNL Tableau]連接到查詢服務

本檔案涵蓋將Tableau與Adobe Experience Platform [!DNL Query Service]連接的步驟。

>[!NOTE]
>
> 本指南假定您已經擁有[!DNL Tableau]的訪問權限，並熟悉如何導航其介面。 有關[!DNL Tableau]的更多資訊，請參閱[official [!DNL Tableau] 文檔](https://help.tableau.com/current/pro/desktop/en-us/default.htm)。

要將[!DNL Tableau]連接到[!DNL Query Service]，請開啟[!DNL Tableau]，並在&#x200B;**[!DNL To a Server]**&#x200B;部分中選擇&#x200B;**[!DNL More]** ，然後選擇&#x200B;**[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

您現在可以輸入值以連接Adobe Experience Platform。 有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請訪問Platform](https://platform.adobe.com/query/configuration)上的[ credentials頁。 要查找憑據，請登錄到[!DNL Platform]，然後選擇&#x200B;**[!UICONTROL 查詢]**，然後選擇&#x200B;**[!UICONTROL 憑據]**。

在嘗試連接之前，請確保已選中「**[!UICONTROL SSL Required]**」框。

填寫完所有憑據後，選擇&#x200B;**[!DNL Sign In]**&#x200B;繼續。

![](../images/clients/tableau/sign-in.png)

您現在已連線Adobe Experience Platform，並在旁邊顯示表格清單。

![](../images/clients/tableau/connected.png)

## 後續步驟

現在您已連接[!DNL Query Service]，您可以使用[!DNL Tableau]來編寫查詢。 有關如何寫入和運行查詢的詳細資訊，請閱讀[運行查詢](../best-practices/writing-queries.md)的指南。