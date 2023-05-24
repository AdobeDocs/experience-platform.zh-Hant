---
keywords: 廣告；交易部門；廣告貿易台
title: 交易台連接
description: 交易台是一個自助服務平台，供廣告購買者跨顯示器、視頻和移動庫存來源執行重定目標和受眾定向數字活動。
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 2%

---

# [!DNL The Trade Desk] 連接

## 總覽 {#overview}

[!DNL The Trade Desk] 目標可幫助您將配置檔案資料發送到 [!DNL The Trade Desk]。

[!DNL The Trade Desk] 是一個自助服務平台，供廣告購買者跨顯示器、視頻和移動清點源執行重定向和受眾定向的數字活動。

將配置檔案資料發送到 [!DNL Trade Desk]，必須首先連接到目標。

## 使用案例 {#use-cases}

作為營銷人員，我希望能夠使用 [!DNL Trade Desk IDs] 或設備ID，以建立重定向或受眾定向的數字活動。

## 支援的身份 {#supported-identities}

[!DNL The Trade Desk] 支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| 交易台ID | 交易台平台中的廣告商ID |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在將段（受眾）的所有成員導出到目標。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>如果您希望建立第一個目標 [!DNL The Trade Desk] 還沒啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在過去的Experience CloudID服務中(與Adobe Audience Manager或其他應用程式一起)，請聯繫Adobe咨詢或客戶服務以啟用ID同步。 如果你之前 [!DNL The Trade Desk] Audience Manager中的整合，您設定的ID同步將傳遞到平台。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 帳戶ID]**:您 [!DNL Trade Desk] [!UICONTROL 帳戶ID]。
* **[!UICONTROL 伺服器位置]**:詢問 [!DNL Trade Desk] 代表您應使用的區域伺服器。 這些是可供您選擇的區域伺服器：
   * **[!UICONTROL 歐洲]**
   * **[!UICONTROL 新加坡]**
   * **[!UICONTROL 東京]**
   * **[!UICONTROL 東北美洲]**
   * **[!UICONTROL 北美西部]**
   * **[!UICONTROL 拉丁美洲]**

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到流段導出目標](../../ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

在 [段計畫](../../ui/activate-segment-streaming-destinations.md#scheduling) 步驟，必須手動將段映射到目標平台中相應的ID或友好名稱。

在映射段時，我們建議您使用平台段名稱或更短形式的段名稱，以方便使用。 但是，目標中的段ID或名稱不需要與平台帳戶中的段ID或名稱匹配。 在映射欄位中插入的任何值都將由目標反映。

如果使用多個設備映射(cookie ID), [!DNL IDFA]。 [!DNL GAID])，確保對所有三個映射使用相同的映射值。 [!DNL The Trade Desk] 將將所有資料集合到單個資料段，並進行設備級故障分析。

![段映射ID](../../assets/common/segment-mapping-id.png)

## 導出的資料 {#exported-data}

驗證資料是否已成功導出到 [!DNL The Trade Desk] 目標，檢查 [!DNL Trade Desk] 帳戶。 如果激活成功，則會在您的帳戶中填充受眾。
