---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Azure事件集線器來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 1%

---


# 在UI中 [!DNL Azure Event Hubs] 建立來源連接器

>[!NOTE]
> 連接 [!DNL Azure Event Hubs] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用使 [!DNL Azure Event Hubs] 用者介面驗證(以下稱[!DNL Event Hubs]為「」)來源連接器 [!DNL Platform] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [體驗資料模型(XDM)系統](../../../../../xdm/home.md): 組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   - [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
- [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經擁有 [!DNL Event Hubs] 帳戶，則可以略過本文檔的其餘部分，然後繼續有關配置資料 [流的教程](../../dataflow/streaming/cloud-storage.md)。

### 收集必要的認證

要驗證源連接器， [!DNL Event Hubs] 必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `sasKeyName` | 授權規則的名稱，也稱為SAS密鑰名稱。 |
| `sasKey` | 產生的共用存取簽名。 |
| `namespace` | 您存取的 [!DNL Event Hubs] 命名空間。 |

有關這些值的詳細資訊，請參 [閱此Event Hub文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。

## 連線您的帳 [!DNL Event Hubs] 戶

收集完所需的認證後，您可依照下列步驟將帳戶連結 [!DNL Event Hubs] 至 [!DNL Platform]。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 ** Sources工作區。 「目 *[!UICONTROL 錄]* 」頁籤顯示可連接到的各種源 [!DNL Platform]。 每個來源顯示與其關聯的現有帳戶數。

在「雲 *[!UICONTROL 端儲存空間]* 」類別下，選取「 **[!UICONTROL Azure事件集線器]** 」並按一 **下「+」圖示(+)** ，以建立新的事件集線器連接器。

![](../../../../images/tutorials/create/eventhub/catalog.png)

出現 *[!UICONTROL 「連接到Azure事件集線器]* 」對話框。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在顯示的輸入表單上，提供名稱、可選說明和您的事件集線器憑據。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![](../../../../images/tutorials/create/eventhub/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的事件集線器帳戶，然後選擇「下 **[!UICONTROL 一步]** 」繼續。

![](../../../../images/tutorials/create/eventhub/existing.png)

## 後續步驟

通過本教程，您已將事件集線器帳戶連接到 [!DNL Platform]。 您現在可以繼續下一個教學課程，並 [設定資料流，將雲端儲存空間的資料匯入平台](../../dataflow/streaming/cloud-storage.md)。