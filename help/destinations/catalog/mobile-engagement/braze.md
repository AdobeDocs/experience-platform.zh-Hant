---
keywords: 移動；曬；消息；
title: Braze連接
description: Braze是一個全面的客戶參與平台，為客戶和他們喜愛的品牌之間提供相關而令人難忘的體驗。
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 1%

---

# [!DNL Braze] 連接

## 總覽 {#overview}

的 [!DNL Braze] 目標可幫助您將配置檔案資料發送到 [!DNL Braze]。

[!DNL Braze] 是一個全面的客戶參與平台，為客戶與他們所喜愛的品牌之間提供相關且令人難忘的體驗。

將配置檔案資料發送到 [!DNL Braze]，必須首先連接到目標。

## 目標說明 {#specifics}

請注意以下特定於 [!DNL Braze] 目標：

* [!DNL Adobe Experience Platform] 段導出到 [!DNL Braze] 下 `AdobeExperiencePlatformSegments` 屬性。

>[!NOTE]
>
>請記住，將其他自定義屬性發送到 [!DNL Braze] 可能會導致 [!DNL Braze] 資料點消耗。 請咨詢您的 [!DNL Braze] 客戶經理，然後再發送其他自定義屬性。

## 使用案例 {#use-cases}

作為營銷人員，我希望瞄準移動項目目標中的用戶，並內置分段 [!DNL Adobe Experience Platform]。 此外，我希望根據他們的屬性為他們提供個性化體驗 [!DNL Adobe Experience Platform] 配置檔案，一旦在中更新段和配置檔案 [!DNL Adobe Experience Platform]。

## 支援的身份 {#supported-identities}

[!DNL Braze] 支援激活下表中描述的身份。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| 外部ID | 自定義 [!DNL Braze] 支援任何標識映射的標識符。 | 您可以發送任何 [身份](../../../identity-service/namespaces.md) 到 [!DNL Braze] 目標，只要你將其映射到 [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation)。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：根據您的欄位映射，發送電子郵件地址、電話號碼、姓氏)和/或身份。[!DNL Adobe Experience Platform] 段導出到 [!DNL Braze] 下 `AdobeExperiencePlatformSegments` 屬性。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

要驗證到目標，請填寫必填欄位並選擇 **[!UICONTROL 連接到目標]**。

* **[!UICONTROL Braze帳戶令牌]**:這是你的 [!DNL Braze] [!DNL API] 按鈕 您可以找到有關如何獲取 [!DNL API] 此處的鍵： [REST API密鑰概述](https://www.braze.com/docs/api/api_key/)。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:輸入將來用於識別此目標的名稱。
* **[!UICONTROL 說明]**:輸入將幫助您在將來確定此目標的說明。
* **[!UICONTROL 終結點實例]**:請 [!DNL Braze] 代表您應使用的終結點實例。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到流段導出目標](../../ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

## 映射注意事項 {#mapping-considerations}

正確發送受眾資料 [!DNL Adobe Experience Platform] 到 [!DNL Braze] 目標，您需要完成欄位映射步驟。

映射包括在 [!DNL Experience Data Model] (XDM)中的架構欄位 [!DNL Platform] 帳戶，以及目標目標中對應的等價項。

正確將XDM欄位映射到 [!DNL Braze] 目標欄位，請執行以下步驟：

在 [!UICONTROL 映射] 按一下 **[!UICONTROL 添加新映射]**。

![製作目標添加映射](../../assets/catalog/mobile-engagement/braze/mapping.png)

在 [!UICONTROL 源欄位] 的子菜單。

![佈雷茲目標源映射](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

在 [!UICONTROL 選擇源欄位] 窗口中，您可以在兩個類別的XDM欄位中進行選擇：
* [!UICONTROL 選擇屬性]:使用此選項將特定欄位從XDM架構映射到 [!DNL Braze] 屬性。

![佈雷茲目標映射源屬性](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL 選擇標識命名空間]:使用此選項映射 [!DNL Platform] 標識命名空間到 [!DNL Braze] 命名空間。

![佈雷茲目標映射源命名空間](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

選擇源欄位，然後按一下 **[!UICONTROL 選擇]**。

在 [!UICONTROL 目標欄位] 的子菜單。

![佈雷茲目標映射](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

在 [!UICONTROL 選擇目標欄位] 窗口，您可以在兩個類別的目標欄位中進行選擇：
* [!UICONTROL 選擇標識命名空間]:使用此選項映射 [!DNL Platform] 標識命名空間 [!DNL Braze] 標識命名空間。
* [!UICONTROL 選擇自定義屬性]:使用此選項將XDM屬性映射到自定義 [!DNL Braze] 您在 [!DNL Braze] 帳戶。 <br> 也可以使用此選項將現有XDM屬性更名為 [!DNL Braze]。 例如，映射 `lastName` 自定義的XDM屬性 `Last_Name` 屬性 [!DNL Braze]，將建立 `Last_Name` 屬性 [!DNL Braze]，並映射 `lastName` XDM屬性。

![製作目標映射欄位](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

選擇目標欄位，然後按一下 **[!UICONTROL 選擇]**。

您現在應該在清單中看到您的欄位映射。

![Braze目標映射完成](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

要添加更多映射，請重複上述步驟。

## 映射示例 {#mapping-example}

假設您的XDM配置檔案架構和 [!DNL Braze] 實例包含以下屬性和標識：

|  | XDM配置檔案架構 | [!DNL Braze] 例項 |
|---|---|---|
| 屬性 | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>名字</code></li><li>姓氏</code></li><li>電話號碼</code></li></ul> |
| 身分 | <ul><li>電子郵件</code></li><li>Google廣告ID(GAID)</code></li><li>Apple廣告商ID</code></li></ul> | <ul><li>外部ID</code></li></ul> |

正確的映射如下所示：

![佈雷茲目標映射示例](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## 導出的資料 {#exported-data}

驗證資料是否已成功導出到 [!DNL Braze] 目標，檢查 [!DNL Braze] 帳戶。 [!DNL Adobe Experience Platform] 段導出到 [!DNL Braze] 下 `AdobeExperiencePlatformSegments` 屬性。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](../../../data-governance/home.md)。
