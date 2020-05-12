---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Amazon Kinesis源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 1eb6883ec9b78e5d4398bb762bba05a61c0f8308
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---


# 在UI中建立Amazon Kinesis源連接器

>[!NOTE]
> Amazon Kinesis連接器正在測試中。 功能和檔案可能會有所變更。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教程提供了使用平台用戶介面驗證Amazon Kinesis（以下稱為「Kinesis」）源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   - [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
- [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經擁有Kinesis帳戶，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/streaming/cloud-storage.md)。

### 收集必要的認證

要驗證Kinesis源連接器，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `accessKeyId` | Kinesis帳戶的訪問密鑰ID。 |
| `Secret access key` | Kinesis帳戶的秘密訪問密鑰。 |
| `region` | 您的AWS伺服器所在地區。 |

有關這些值的詳細資訊，請參 [閱本Kinesis文檔](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)。

## 連接Kinesis帳戶

收集到所需憑據後，可以按照以下步驟將Kinesis帳戶連結到平台。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **Sources** ，以存取 ** Sources工作區。 「目 *錄* 」標籤會顯示可連接至「平台」的各種來源。 每個來源顯示與其關聯的現有帳戶數。

在「雲 *儲存* 」類別下，選擇 **Amazon Kinesis** ，然 **後按一下+表徵圖(+)** ，建立新的Kinesis連接器。

![](../../../../images/tutorials/create/eventhub/catalog.png)

此時 *將顯示「連接到Amazon Kinesis* 」對話框。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **帳戶」**。 在顯示的輸入表單上，提供名稱、可選說明和Kinesis憑據。 完成後，選擇 **Connect** ，然後為建立新連接留出一些時間。

![](../../../../images/tutorials/create/eventhub/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的Kinesis帳戶，然後選擇「下 **一步** 」繼續。

![](../../../../images/tutorials/create/eventhub/existing.png)

## 後續步驟

通過本教程，您已將Kinesis帳戶連接到平台。 您現在可以繼續下一個教學課程，並 [設定資料流，將雲端儲存空間的資料匯入平台](../../dataflow/streaming/cloud-storage.md)。