---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Azure事件集線器來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 855f543a1cef394d121502f03471a60b97eae256
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# 在UI中建立Azure事件集線器來源連接器

>[!NOTE]
> Azure事件集線器連接器處於測試狀態。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用平台使用者介面驗證Azure事件集線器（以下稱為「事件集線器」）來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   - [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
- [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經擁有Event Hub帳戶，則可以跳過本文檔的其餘部分，並繼續有關配置資料流 [的教程](../../dataflow/streaming/cloud-storage.md)。

### 收集必要的認證

要驗證事件集線器源連接器，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `sasKeyName` | 授權規則的名稱，也稱為SAS密鑰名稱。 |
| `sasKey` | 產生的共用存取簽名。 |
| `namespace` | 您正在訪問的事件集線器的名稱空間。 |

有關這些值的詳細資訊，請參 [閱此Event Hub文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。

## 連接您的事件集線器帳戶

收集完所需憑證後，您可以遵循下列步驟，將您的「事件中樞」帳戶連結至平台。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **Sources** ，以存取 ** Sources工作區。 「目 *錄* 」標籤會顯示可連接至「平台」的各種來源。 每個來源顯示與其關聯的現有帳戶數。

在「雲 *端儲存空間* 」類別下，選取「 **Azure事件集線器** 」並按一 **下「+」圖示(+)** ，以建立新的事件集線器連接器。

![](../../../../images/tutorials/create/eventhub/catalog.png)

出現 *「連接到Azure事件集線器* 」對話框。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **帳戶」**。 在顯示的輸入表單上，提供名稱、可選說明和您的事件集線器憑據。 完成後，選擇 **Connect** ，然後為建立新連接留出一些時間。

![](../../../../images/tutorials/create/eventhub/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的事件集線器帳戶，然後選擇「下 **一步** 」繼續。

![](../../../../images/tutorials/create/eventhub/existing.png)

## 後續步驟

通過本教程，您已將事件集線器帳戶連接到平台。 您現在可以繼續下一個教學課程，並 [設定資料流，將雲端儲存空間的資料匯入平台](../../dataflow/streaming/cloud-storage.md)。