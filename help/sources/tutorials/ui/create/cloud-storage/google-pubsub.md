---
keywords: Experience Platform;home；熱門主題；Google PubSub;google pubsub
solution: Experience Platform
title: 在UI中建立Google PubSub來源連線
topic: 概述
type: 教學課程
description: 瞭解如何使用平台使用者介面建立Google PubSub來源連接器。
translation-type: tm+mt
source-git-commit: 0af90253f04377149986aedf2e9d3012ca06d4f8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# 在UI中建立[!DNL Google PubSub]源連接

>[!NOTE]
>
> [!DNL Google PubSub]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

本教學課程提供使用平台使用者介面建立[!DNL Google PubSub]（以下稱為「[!DNL PubSub]」）的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

如果您已經有有效的[!DNL PubSub]連接，則可跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集必要的認證

要將[!DNL PubSub]連接到平台，您必須為以下憑據提供有效值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `projectId` | 驗證[!DNL PubSub]所需的項目ID。 |
| `credentials` | 驗證[!DNL PubSub]所需的憑證或金鑰。 |

如需這些值的詳細資訊，請參閱下列[PubSub authentication](https://cloud.google.com/pubsub/docs/authentication)檔案。

收集完所需憑證後，您可依照下列步驟將[!DNL Blob]帳戶連結至平台。

## 連接您的[!DNL PubSub]帳戶

在[平台UI](https://platform.adobe.com)中，從左側導覽列選擇&#x200B;**[!UICONTROL 源]**&#x200B;以存取[!UICONTROL 源]工作區。 [!UICONTROL Catalog]畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列，找到您要使用的特定來源。

在[!UICONTROL 雲端儲存區]類別下，選取&#x200B;**[!UICONTROL Google PubSub]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![目錄](../../../../images/tutorials/create/google-pubsub/catalog.png)

此時會顯示「連線至Google PubSub ]**」頁面。**[!UICONTROL &#x200B;在此頁上，您可以使用新認證或現有認證。

### 現有帳戶

要使用現有帳戶，請選擇要建立新資料流的[!DNL PubSub]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![現有](../../../../images/tutorials/create/google-pubsub/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇&#x200B;**[!UICONTROL 新建帳戶]**，然後在輸入表單中提供名稱、可選說明和[!DNL PubSub]驗證憑據。 完成後，選擇&#x200B;**[!UICONTROL 連接到源]** ，然後允許新連接建立一段時間。

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## 後續步驟

在本教學課程後，您將在[!DNL PubSub]帳戶和平台之間建立連接。 您現在可以繼續下一個教學課程，並[設定資料流，將雲端儲存空間的串流資料匯入Platform](../../dataflow/streaming/cloud-storage-streaming.md)。
