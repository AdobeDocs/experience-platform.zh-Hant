---
keywords: Experience Platform；首頁；熱門主題；tableau;Tableau；查詢服務；查詢服務；連線至查詢服務；
solution: Experience Platform
title: 將 Tableau 連接至查詢服務
topic-legacy: connect
description: 本檔案會逐步說明將Tableau與Adobe Experience Platform Query Service連線的步驟。
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 2%

---

# Connect [!DNL Tableau] 查詢服務

本檔案涵蓋連接 [!DNL Tableau] 搭配Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> 本指南假設您已擁有 [!DNL Tableau] 並熟悉如何導覽其介面。 有關 [!DNL Tableau] 可在 [官方 [!DNL Tableau] 檔案](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

連接 [!DNL Tableau] to [!DNL Query Service]，開啟 [!DNL Tableau]，和 **[!DNL To a Server]** 節選 **[!DNL More]** 後跟 **[!DNL PostgreSQL]**

![此 [!DNL Tableau] 控制面板，包含更多 [!DNL PostgreSQL] 突出顯示。](../images/clients/tableau/open-connection.png)

您現在可以輸入值以連線至Adobe Experience Platform。 有關查找資料庫名稱、主機、埠和登錄憑據的詳細資訊，請閱讀 [認證指南](../ui/credentials.md). 若要尋找憑證，請登入 [!DNL Platform]，然後選取 **[!UICONTROL 查詢]**，後跟 **[!UICONTROL 憑證]**.

請確定您已核取 **[!UICONTROL 需要SSL]** 框，然後嘗試連接。

>[!IMPORTANT]
>
>請參閱 [[!DNL Query Service] SSL檔案](./ssl-modes.md) 了解協力廠商連線至Adobe Experience Platform Query Service的SSL支援，以及如何使用 `verify-full` SSL模式。

![此 [!DNL PostgreSQL] 連線對話方塊中填入連線詳細資訊。](../images/clients/tableau/sign-in.png)

>[!IMPORTANT]
>
>第三方BI工具中的巢狀資料結構可以平面化，以改善其可用性，並減少擷取、分析、轉換和報告資料所需的工作量。 請參閱[`FLATTEN` 功能](../best-practices/flatten-nested-data.md) 有關在連接到資料庫時如何激活此設定的說明。

填寫所有憑證後，請選取 **[!DNL Sign In]** 繼續。

您現在已連線Adobe Experience Platform，側面會顯示表格清單。

![新 [!DNL Tableau] 控制面板，左側面板中強調顯示「查詢服務」表格。](../images/clients/tableau/connected.png)

## 後續步驟

既然你已經和 [!DNL Query Service]，您可以使用 [!DNL Tableau] 來寫入查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢](../best-practices/writing-queries.md).
