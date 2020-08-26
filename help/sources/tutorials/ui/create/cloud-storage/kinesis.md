---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Amazon Kinesis源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---


# 在UI中 [!DNL Amazon Kinesis] 建立來源連接器

>[!NOTE]
>
>連接 [!DNL Amazon Kinesis] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用使用者介 [!DNL Amazon Kinesis] 面驗證(以下稱 [!DNL "Kinesis"]為)來源連接器 [!DNL Platform] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [[!DNL Experience Data Model] (XDM)系統](../../../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   - [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
- [[!DNL即時客戶基本資料]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的 [!DNL Kinesis] 連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/streaming/cloud-storage.md)。

### 收集必要的認證

要驗證源連接器， [!DNL Kinesis] 必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `accessKeyId` | 您帳戶的存取金鑰 [!DNL Kinesis] ID。 |
| `Secret access key` | 您帳戶的機密存取 [!DNL Kinesis] 金鑰。 |
| `region` | 您的AWS伺服器所在地區。 |

有關這些值的詳細資訊，請參 [ [!DNL Kinesis] 閱本文檔](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)。

## 連線您的帳 [!DNL Kinesis] 戶

收集完所需的認證後，您可依照下列步驟將帳戶連結 [!DNL Kinesis] 至 [!DNL Platform]。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 **** Sources工作區。 「目 **[!UICONTROL 錄]** 」畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「雲存 **[!UICONTROL 儲」類別下]** ，選擇 **[!UICONTROL Amazon Kinesis]**。 如果這是您第一次使用此連接器，請選擇「配 **[!UICONTROL 置」]**。 否則，請選 **[!UICONTROL 擇「添加資料]** 」(Add data [!DNL Kinesis] )以建立新連接器。

![](../../../../images/tutorials/create/kinesis/catalog.png)

此時 **[!UICONTROL 將顯示「連接到Amazon Kinesis]** 」對話框。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供名稱、選用說明和您的認 [!DNL Kinesis] 證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![](../../../../images/tutorials/create/kinesis/new.png)

### 現有帳戶

若要連線現有帳戶，請選 [!DNL Kinesis] 取您要連線的帳戶，然後選取「下 **[!UICONTROL 一]** 步」繼續。

![](../../../../images/tutorials/create/kinesis/existing.png)

## 後續步驟

透過本教學課程，您已將帳戶連 [!DNL Kinesis] 線至 [!DNL Platform]。 您現在可以繼續下一個教學課程，並 [設定資料流，將雲端儲存空間的資料匯入 [!DNL Platform]](../../dataflow/streaming/cloud-storage.md)。