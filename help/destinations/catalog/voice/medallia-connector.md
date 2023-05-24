---
title: Medallia連接
description: 激活針對Medallia調查和反饋收集的配置檔案，以便更好地瞭解客戶需求和期望。
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 1%

---

# Medallia連接

## 總覽 {#overview}

激活針對Medallia調查和反饋收集的配置檔案，以便更好地瞭解客戶需求和期望。

>[!IMPORTANT]
>
>此文檔頁面由Medallia團隊建立。 如有任何查詢或更新請求，請直接聯繫他們，網址為adobe-integrations@medallia.com。

## 使用案例 {#use-cases}

為了幫助您更好地瞭解您應該如何以及何時使用Medallia目標，以下是Adobe Experience Platform客戶可以使用此目標解決的示例使用案例。

### 用例#1

一個B2B品牌希望評估並簡化其登機計畫。 他們希望將個性化調查即時發送給剛剛完成登機過程的客戶。

### 用例#2

零售商希望更好地瞭解客戶對訂單履行的偏好。 他們希望向過去一個月在網上和店內購買商品的客戶發送一個簡短的1問簡訊調查。

## 先決條件 {#prerequisites}

建立Medallia連接需要以下資訊：
* **OAuth令牌終結點URL**
* **客戶端ID**
* **客戶端密碼**
* **API網關URL**
* **導入API名稱**

與您的Medallia交付團隊合作以獲取這些詳細資訊。

## 支援的身份 {#supported-identities}

Medallia支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 電子郵件地址 | 在您要發送電子郵件邀請調查時，選擇電子郵件目標標識。 當配置檔案與多個電子郵件地址關聯時，Medallia將僅觸發對第一封電子郵件的邀請。 |
| phone | 電話號碼以E.164格式散列 | 當要發送基於SMS的調查時，選擇電話目標標識。 電話號碼必須採用E.164格式，其中包括加號(+)、國際國家/地區呼叫代碼、本地區代碼和電話號碼。 例如：(+)（國家/地區代碼）（區號）（電話號碼）。 當配置檔案與多個電話號碼關聯時，Medallia將僅觸發對第一個電話號碼的邀請。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有新限定成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

要驗證到目標，請填寫必填欄位並選擇 **[!UICONTROL 連接到目標]**。

* **[!UICONTROL OAuth令牌終結點URL]**:通常採用https://instance.medallia.tld/oauth/tenant/token的形式。
* **[!UICONTROL 客戶端ID]**:從你的Medallia派送小組獲得。
* **[!UICONTROL 客戶端密碼]**:從你的Medallia派送小組獲得。

![顯示此目標的驗證螢幕的影像。](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL API網關URL]**:從你的Medallia派送小組獲得。 通常採用https://instance-tenant.apis.medallia.com的形式。
* **[!UICONTROL 導入API名稱]**:從你的Medallia派送小組獲得。 此連接中要使用的Medallia導入API（也稱為Web源）的名稱。 您可以激活不同的段到不同的導入API以觸發不同的調查程式。

![顯示此目標的目標詳細資訊螢幕的影像。](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

### 映射屬性和標識 {#map}

必鬚根據使用情形映射以下目標標識命名空間：
* 對於基於電子郵件的調查， **電子郵件** 必須映射為目標欄位 **目標欄位** > **選擇標識命名空間** > **電子郵件**
* 對於簡訊調查， **電話** 必須映射為目標欄位 **目標欄位** > **選擇標識命名空間** > **電話**。 電話號碼必須採用E.164格式，包括加號(+)、國際國家/地區呼叫代碼、本地區代碼和電話號碼

強烈建議您還應映射其他目標自定義屬性以建立個性化調查，並將有關客戶的附加資訊附加到調查記錄：

* 個性化調查通常按名稱向客戶提供服務
   * 將客戶的名字映射到 **目標欄位** > **選擇自定義屬性** > **屬性名稱** > **名字**
   * 將客戶的姓映射到 **目標欄位** > **選擇自定義屬性** > **屬性名稱** > **lastname**
* 根據需要為任何其他目標自定義屬性添加映射

![顯示標識和屬性的示例映射的影像。](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> 與您的Medallia交付團隊共用 **屬性名稱** 用於映射的每個目標自定義屬性 **目標欄位** > **選擇自定義屬性** > **屬性名稱**。 您可能希望拍攝映射頁面的螢幕快照以直接共用。

## 導出的資料 {#exported-data}

在將段激活到目標後，通知您的Medallia交付團隊，該團隊將能夠驗證從Adobe Experience Platform到Medallia的導出資料。 注意，調查只有在成功進行資料覈實後才能在Medallia內激活；在此之前，資料將導出到Medallia，但不會觸發對客戶的調查。

下面提供了導出資料的示例JSON，它使用中的上面螢幕快照中的示例映射 **映射屬性和標識** 部分：

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  “John” ,
        "lastname":  “Smith”,
        "contactId": "jsmith120002",
    }
]
```

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。
