---
title: Pinterest客戶清單連接
description: 從您的客戶清單、訪問您站點的人員或已與您的內容在Pinterest進行互動的人員中建立受眾。
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 3%

---

# [!DNL Pinterest Customer List] 連接

## 總覽 {#overview}

從您的客戶清單、訪問您站點的人員或已與您的內容在Pinterest進行互動的人員中建立受眾。

>[!IMPORTANT]
>
>這個目的地是Pinterest隊建的。 如有任何查詢或更新請求，請直接聯繫他們，網址為https://help.pinterest.com/en/contact。

## 先決條件 {#prerequisites}

* 用戶需要向具有訪問其要向其添加受眾的廣告商帳戶的Pinterest帳戶進行身份驗證。 有關共用廣告商帳戶的詳細資訊 [這裡](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts)。 具體來說，用戶需要「受眾」訪問級別。
* 有關客戶清單標識格式的詳細資訊 [這裡](https://help.pinterest.com/en/business/article/audience-targeting)。

## 支援的身份 {#supported-identities}

的 [!DNL Pinterest Customer List] 目標支援激活下表中描述的身份。 瞭解有關 [身份](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)。

在 [映射步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 目標激活工作流中，將所需標識映射到目標欄位 *pinterest觀眾*。 身份在資料接收到Pinterest後被區分和解決。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 映射 *GAID* 目標標識欄位的源標識名稱空間 *pinterest觀眾*。 身份在資料接收到Pinterest後被區分和解決。 |
| IDFA | [!DNL Apple ID for Advertisers] | 映射 *IDFA* 目標標識欄位的源標識名稱空間 *pinterest觀眾*。 身份在資料接收到Pinterest後被區分和解決。 |
| 電子郵件 | 電子郵件地址（明文或使用SHA256算法散列） | 純文字檔案和SHA256散列電子郵件地址都受Adobe Experience Platform支援。 <br> 映射 *電子郵件* 或 *Email_LC_SHA256* 目標標識欄位的源標識名稱空間 *pinterest觀眾*。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中包含在Pinterest客戶清單目標中使用的標識符（名稱、電話號碼或其他）。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 使用案例 {#use-cases}

幫助您更好地瞭解您應如何以及何時使用 [!DNL Pinterest Customer List] 目的地，以下是Adobe Experience Platform客戶可通過使用此目的地解決的示例使用案例。

### 用例#1

從您的客戶清單、訪問您站點的人員或已與您的內容在Pinterest進行互動的人員中建立受眾。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 廣告商ID]**:您的Pinterest廣告商ID。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)。

## 其他資源 {#additional-resources}

請參閱 [Pinterest幫助中心頁](https://help.pinterest.com/en/business/article/audience-targeting) 的雙曲餘切值。
