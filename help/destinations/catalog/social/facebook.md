---
keywords: facebook連接；facebook連接；facebook目的地；facebook;instagram；信使；facebook信使
title: Facebook連接
description: 啟用您Facebook宣傳的個人檔案，根據雜湊的電子郵件鎖定受眾、個人化和抑制受眾。
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
translation-type: tm+mt
source-git-commit: 01aed33913b5334263090aea17f75ce181717c50
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 2%

---

# [!DNL Facebook] 連接

## 概述 {#overview}

啟用[!DNL Facebook]促銷活動的設定檔，以便根據雜湊的電子郵件鎖定受眾、個人化和抑制受眾。

您可以將此目標用於[!DNL Facebook’s]系列應用程式（包括[!DNL Facebook]、[!DNL Instagram]、[!DNL Audience Network]和[!DNL Messenger]）中的受眾定位。 [!DNL Custom Audiences]在 [!DNL Facebook Ads Manager] 中的廣告版位層級會指出您選擇針對哪個應用程式執行行銷活動。

![FacebookAdobe Experience PlatformUI的目的地](../../assets/catalog/social/facebook/catalog.png)

## 使用個案

為協助您進一步瞭解如何及何時使用[!DNL Facebook]目標，以下是Adobe Experience Platform客戶可使用此功能解決的兩個範例使用案例。

### 使用案例#1

線上零售商想透過社交平台接觸現有客戶，並根據先前的訂單向他們展示個人化優惠。 線上零售商可將其CRM的電子郵件位址收錄至Adobe Experience Platform，從其線下資料建立區段，並將這些區段傳送至[!DNL Facebook]社交平台，以最佳化其廣告支出。

### 使用案例#2

航空公司有不同的客戶層級（銅、銀和金），並希望透過社交平台為每個層級提供個人化優惠。 不過，並非所有客戶都使用該航空公司的行動應用程式，其中有些客戶尚未登入該公司網站。 公司對於這些客戶的唯一識別碼是會籍ID和電子郵件地址。

若要跨社交媒體鎖定客戶，他們可以將客戶資料從CRM載入Adobe Experience Platform，將電子郵件地址當做識別碼。

接著，他們可以使用離線資料（包括相關的會籍ID和客戶層級）來建立新的受眾細分，以便透過[!DNL Facebook]目標鎖定。

## [!DNL Facebook]目標{#data-governance}的資料控管

>[!IMPORTANT]
>
>傳送至[!DNL Facebook]的資料不能包含銜接身分。 您有責任履行此義務，並可確保選定進行啟動的區段不會在其合併政策中使用拼接選項來履行此義務。 進一步瞭解[合併策略](/help/profile/ui/merge-policies.md)。

## 支援的身分{#supported-identities}

[!DNL Facebook Custom Audiences] 支援啟用下表所述的身分。進一步瞭解[identities](/help/identity-service/namespaces.md)。

| 目標識別 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當您的來源識別為GAID命名空間時，請選取GAID目標識別。 |
| IDFA | 廣告商的Apple ID | 當您的來源識別為IDFA命名空間時，請選取IDFA目標識別。 |
| phone_sha256 | 使用SHA256演算法雜湊電話號碼 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的說明，分別為純文字檔案和雜湊電話號碼使用適當的命名空間。 當來源欄位包含未雜湊屬性時，請勾選&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 請依照[ID符合要求](#id-matching-requirements-id-matching-requirements)區段中的指示，並分別針對純文字和雜湊電子郵件地址使用適當的名稱空間。 當來源欄位包含未雜湊屬性時，請勾選&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。 |
| extern_id | 自訂使用者ID | 當您的來源識別為自訂命名空間時，請選取此目標識別。 |

## 導出類型{#export-type}

**區段匯出** -您正匯出區段（對象）的所有成員，並使用Facebook目的地所使用的識別碼（名稱、電話號碼或其他）。

## Facebook帳戶先決條件{#facebook-account-prerequisites}

在將對象區段傳送至[!DNL Facebook]之前，請確定您符合下列需求：

- 您的[!DNL Facebook]使用者帳戶必須已針對您計畫使用的廣告帳戶啟用&#x200B;**[!DNL Manage campaigns]**&#x200B;權限。
- **Adobe Experience Cloud**&#x200B;商業帳戶必須新增為[!DNL Facebook Ad Account]的廣告合作夥伴。 使用 `business ID=206617933627973`。如需詳細資訊，請參閱Facebook檔案中的[將合作夥伴新增至您的業務經理](https://www.facebook.com/business/help/1717412048538897)。
   >[!IMPORTANT]
   >
   > 設定Adobe Experience Cloud的權限時，您必須啟用「管理促銷活動&#x200B;**」權限。**[!DNL Adobe Experience Platform]整合需要權限。
- 閱讀並簽署[!DNL Facebook Custom Audiences]服務條款。 若要這麼做，請前往`https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中`accountID`是您的[!DNL Facebook Ad Account ID]。

## ID匹配要求{#id-matching-requirements}

[!DNL Facebook] 要求不會傳送任何個人識別資訊(PII)。因此，激活至[!DNL Facebook]的觀眾可以鍵入&#x200B;*雜湊*&#x200B;標識符，如電子郵件地址或電話號碼。

您必須依據您收錄至Adobe Experience Platform的ID類型，遵守其相應要求。

## 電話號碼雜湊要求{#phone-number-hashing-requirements}

在[!DNL Facebook]中啟用電話號碼有兩種方法：

- **接收原始電話號碼**:您可以將原始電話號碼以格式 [!DNL E.164] 內嵌 [!DNL Platform]。在啟動時會自動雜湊。 如果您選擇此選項，請務必將原始電話號碼永遠收錄到`Phone_E.164`命名空間中。
- **接收雜湊電話號碼**:您可先將電話號碼雜湊，再將其擷取 [!DNL Platform]。如果您選擇此選項，請務必將雜湊電話號碼永遠收錄到`Phone_SHA256`命名空間中。

>[!NOTE]
>
>不能在[!DNL Facebook]中激活包含在`Phone`名稱空間中的電話號碼。


## 電子郵件散列要求{#email-hashing-requirements}

您可以先將電子郵件地址雜湊，再將其匯入Adobe Experience Platform，或在Experience Platform中清楚使用電子郵件地址，並在啟動時讓[!DNL Platform]雜湊這些地址。

若要瞭解如何在Experience Platform中擷取電子郵件地址，請參閱[批次擷取概觀](/help/ingestion/batch-ingestion/overview.md)和[串流擷取概觀](/help/ingestion/streaming-ingestion/overview.md)。

如果您選擇自行排列電子郵件地址，請務必符合下列要求：

- 從電子郵件字串中修剪所有前導和尾隨空格；範例：`johndoe@example.com`，而非`<space>johndoe@example.com<space>`;
- 在對電子郵件字串進行散列時，請務必對小寫字串進行散列；
   - 範例：`example@email.com`，而非`EXAMPLE@EMAIL.COM`;
- 確保雜湊字串全部為小寫
   - 範例：`55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，而非`55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- 別用鹽鹽。

>[!NOTE]
>
>啟動後，[!DNL Platform]會自動雜湊來自未雜湊名稱空間的資料。
> 屬性來源資料不會自動雜湊。 當來源欄位包含未雜湊屬性時，請勾選&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。
> **[!UICONTROL Apply transformation]**&#x200B;選項僅在選擇屬性作為源欄位時顯示。 當您選擇名稱空間時，不會顯示它。

![身份映射轉換](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 使用自訂名稱空間{#custom-namespaces}

在使用`Extern_ID`命名空間將資料傳送至[!DNL Facebook]之前，請務必使用[!DNL Facebook Pixel]同步您自己的識別碼。 如需詳細資訊，請參閱[Facebook官方檔案](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers)。

## 連接到目標{#connect-destination}

若要連線至[!DNL Facebook]目的地，請參閱[社交網路目的地驗證工作流程](./workflow.md)。

下面的視訊也示範設定[!DNL Facebook]目標及啟用區段的步驟。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## 啟用區段至[!DNL Facebook] {#activate-segments}

如需如何啟用區段至[!DNL Facebook]的指示，請參閱[啟用資料至目標](../../ui/activate-destinations.md)。

在&#x200B;**[!UICONTROL Segment schedule]**&#x200B;步驟中，當將區段傳送至[!DNL Facebook Custom Audiences]時，您必須提供[!UICONTROL Origin of audience]。

![Facebook觀眾源](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## 導出資料{#exported-data}

對於[!DNL Facebook]，成功啟動表示[!DNL Facebook]自訂觀眾將以程式設計方式建立在[[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/)中。 當使用者符合已啟用區段的資格或被取消資格時，會新增及移除觀眾中的區段成員資格。

>[!TIP]
>
>Adobe Experience Platform與[!DNL Facebook]之間的整合支援歷史讀者回填。 當您將區段啟動至目標時，所有歷史區段資格都會傳送至[!DNL Facebook]。
