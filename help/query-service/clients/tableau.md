---
keywords: Experience Platform；首頁；熱門主題；表；表；查詢服務；查詢服務；連接到查詢服務；
solution: Experience Platform
title: 將 Tableau 連接至查詢服務
topic-legacy: connect
description: 本文檔介紹將Tableau與Adobe Experience Platform查詢服務連接的步驟。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: ad3e1b0de6dd3b82cc82f0dc3d0f36b12cd3899e
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 3%

---

# 連接 [!DNL Tableau] 查詢服務

本文檔介紹將Tableau與Adobe Experience Platform連接的步驟 [!DNL Query Service]。

>[!NOTE]
>
> 本指南假定您已具有訪問 [!DNL Tableau] 並熟悉如何導航其介面。 有關 [!DNL Tableau] 在 [官 [!DNL Tableau] 文檔](https://help.tableau.com/current/pro/desktop/en-us/default.htm)。

連接 [!DNL Tableau] 至 [!DNL Query Service]開啟 [!DNL Tableau]的 **[!DNL To a Server]** 節選 **[!DNL More]** 後跟 **[!DNL PostgreSQL]**

![](../images/clients/tableau/open-connection.png)

現在可以輸入值以與Adobe Experience Platform連接。 有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請閱讀 [憑據指南](../ui/credentials.md)。 要查找憑據，請登錄到 [!DNL Platform]，然後選擇 **[!UICONTROL 查詢]**，後跟 **[!UICONTROL 憑據]**。

確保您已檢查 **[!UICONTROL 需要SSL]** 框，然後嘗試連接。

>[!IMPORTANT]
>
>查看 [[!DNL Query Service] SSL文檔](./ssl-modes.md) 瞭解對與Adobe Experience Platform查詢服務的第三方連接的SSL支援，以及如何使用 `verify-full` SSL模式。

填寫完所有憑據後，選擇 **[!DNL Sign In]** 繼續。

![](../images/clients/tableau/sign-in.png)

您現在已與Adobe Experience Platform連接，並在旁邊顯示表清單。

![](../images/clients/tableau/connected.png)

## 後續步驟

既然你已經和 [!DNL Query Service]，您可以使用 [!DNL Tableau] 來編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀上的指南 [運行查詢](../best-practices/writing-queries.md)。
