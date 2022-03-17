---
keywords: '廣告；炳； '
title: Microsoft兵
description: 使用Microsoft必應連接目標，您可以在Microsoft顯示廣告中執行重定目標和針對受眾的數字營銷活動。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 3%

---

# [!DNL Microsoft Bing] 連接 {#bing-destination}

## 總覽 {#overview}

的 [!DNL Microsoft Bing] 目標可幫助您將配置檔案資料發送到 [!DNL Microsoft Display Advertising]。

將配置檔案資料發送到 [!DNL Microsoft Bing]，必須首先連接到目標。

## 使用案例 {#use-cases}

作為營銷人員，我希望能夠使用 [!DNL Microsoft Advertising IDs] 通過顯示廣告向目標用戶 [!DNL Microsoft Advertising] 頻道。

## 支援的身份 {#supported-identities}

[!DNL Microsoft Bing] 支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 |
|---|---|
| 女僕 | Microsoft廣告ID |

{style=&quot;table-layout:auto&quot;}

## 導出類型和頻率 {#export-type-frequency}

**[!DNL Segment Export]**  — 將段（受眾）的所有成員導出到 [!DNL Microsoft Bing] 目標。

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在將段（受眾）的所有成員導出到 [!DNL Microsoft Bing] 目標。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style=&quot;table-layout:auto&quot;&quot;

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>如果您希望建立第一個目標 [!DNL Microsoft Bing] 還沒啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在過去的Experience CloudID服務中(與Adobe Audience Manager或其他應用程式一起)，請聯繫Adobe咨詢或客戶服務以啟用ID同步。 如果你之前 [!DNL Microsoft Bing] Audience Manager中的整合，您設定的ID同步將傳遞到平台。

配置目標時，必須提供以下資訊：

* [!UICONTROL 帳戶ID]:這是 [!DNL Bing Ads CID]，格式為整數。

## 連接到目標 {#connect}

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 帳戶ID]**:您 [!DNL Bing Ads CID]。

## 將段激活到此目標 {#activate}

請參閱 [將受眾資料激活到流段導出目標](../../ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

在 [段計畫](../../ui/activate-segment-streaming-destinations.md#scheduling) 步驟，必須手動將段映射到目標中的相應ID或友好名稱。

在映射段時，建議您使用 [!DNL Platform] 段名稱或更短的形式，以方便使用。 但是，目標中的段ID或名稱不需要與目標中的段ID或名稱匹配 [!DNL Platform] 帳戶。 在映射欄位中插入的任何值都將由目標反映。

## 導出的資料 {#exported-data}

驗證資料是否已成功導出到 [!DNL Microsoft Bing] 目標，檢查 [!DNL Microsoft Bing Ads] 帳戶。 如果激活成功，則會在您的帳戶中填充受眾。
