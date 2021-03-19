---
keywords: Experience Platform;home；熱門主題；Google PubSub;google pubsub
solution: Experience Platform
title: 在UI中建立Google PubSub來源連線
topic: 概述
type: 教學課程
description: 瞭解如何使用平台使用者介面建立Google PubSub來源連接器。
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# 在UI中建立[!DNL Google PubSub]源連接

>[!NOTE]
>
> [!DNL Google PubSub]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

本教學課程提供使用平台使用者介面建立[!DNL Google PubSub]（以下稱為「[!DNL PubSub]」）的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示並增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

如果您已經有有效的[!DNL PubSub]連接，則可跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集必要的認證

要將[!DNL PubSub]連接到平台，您必須為以下憑據提供有效值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `projectId` | 驗證[!DNL PubSub]所需的項目ID。 |
| `credentials` | 驗證[!DNL PubSub]所需的憑證或私密金鑰ID。 |

如需這些值的詳細資訊，請參閱下列[PubSub authentication](https://cloud.google.com/pubsub/docs/authentication)檔案。 如果您使用服務帳戶型驗證，請參閱以下[PubSub指南](https://cloud.google.com/docs/authentication/production#create_service_account)以取得如何產生認證的步驟。

>[!TIP]
>
>如果您使用以服務帳戶為基礎的驗證，請確定您已授與足夠的使用者存取權給您的服務帳戶，而且在複製和貼上認證時，JSON中沒有額外的空格。

收集完所需憑證後，您可依照下列步驟將[!DNL PubSub]帳戶連結至平台。

## 連接您的[!DNL PubSub]帳戶

在[平台UI](https://platform.adobe.com)中，從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL Catalog]畫面會顯示各種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列，找到您要使用的特定來源。

在[!UICONTROL Cloud storage]類別下，選擇&#x200B;**[!UICONTROL Google PubSub]**，然後選擇&#x200B;**[!UICONTROL Add data]**。

![目錄](../../../../images/tutorials/create/google-pubsub/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Connect to Google PubSub]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 現有帳戶

要使用現有帳戶，請選擇要建立新資料流的[!DNL PubSub]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![現有](../../../../images/tutorials/create/google-pubsub/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇&#x200B;**[!UICONTROL New account]**，然後在輸入表單上提供名稱、可選說明和[!DNL PubSub]驗證憑據。 完成後，選擇&#x200B;**[!UICONTROL Connect to source]** ，然後允許一些時間建立新連接。

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## 後續步驟

在本教學課程後，您將在[!DNL PubSub]帳戶和平台之間建立連接。 您現在可以繼續下一個教學課程，並[設定資料流，將雲端儲存空間的串流資料匯入Platform](../../dataflow/streaming/cloud-storage-streaming.md)。
