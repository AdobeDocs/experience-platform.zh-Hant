---
keywords: linkedin連線；linkedin連線；linkedin目的地；linkedin;
title: Linkedin相符的對象連線
description: 根據雜湊電子郵件，啟用LinkedIn行銷活動的設定檔，以鎖定對象、個人化和隱藏。
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---

# [!DNL LinkedIn Matched Audiences] 連接

## 概覽 {#overview}

根據雜湊電子郵件和行動ID，啟用[!DNL LinkedIn]促銷活動的設定檔，以鎖定對象、個人化和隱藏。

![linkedInAdobe Experience Platform UI中的目的地](../../assets/catalog/social/linkedin/catalog.png)

## 使用案例

為協助您更清楚了解使用[!DNL LinkedIn Matched Audiences]目的地的方式和時機，以下是Adobe Experience Platform客戶可透過此功能解決的使用案例。

軟體公司組織會議，希望與參與者保持聯繫，並根據他們的會議出席情況向他們顯示個性化優惠。 公司可將其自己的[!DNL CRM]內嵌電子郵件地址或行動裝置ID至Adobe Experience Platform。 接著，他們可以從自己的離線資料建立區段，並將這些區段傳送至[!DNL LinkedIn]社交平台，最佳化其廣告支出。

## 支援的身分 {#supported-identities}

[!DNL LinkedIn Matched Audiences] 支援啟用下表所述的身分。深入了解[identities](/help/identity-service/namespaces.md)。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當源標識為GAID命名空間時，選擇此目標標識。 |
| IDFA | 廣告商專用的Apple ID | 當您的來源識別為IDFA命名空間時，請選取此目標識別。 |
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 請依照[ID符合需求](#id-matching-requirements-id-matching-requirements)一節中的指示，並分別針對純文字和雜湊電子郵件使用適當的命名空間。 當源欄位包含未雜湊屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。 |


## 匯出類型 {#export-type}

**區段匯出**  — 您會匯出區段（對象）的所有成員，以及目的地中使用的識別碼(名稱、電話號碼及其他 [!DNL LinkedIn Matched Audiences] )。

## linkedIn帳戶必要條件 {#LinkedIn-account-prerequisites}

在使用[!UICONTROL LinkedIn相符對象]目的地之前，請確定您的[!DNL LinkedIn Campaign Manager]帳戶具有[!DNL Creative Manager]權限層級或更高。

若要了解如何編輯您的[!DNL LinkedIn Campaign Manager]使用者權限，請參閱LinkedIn檔案中的[新增、編輯及移除Advertising帳戶的使用者權限](https://www.linkedin.com/help/lms/answer/5753)。

## ID比對需求 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] 需要清楚傳送任何個人識別資訊(PII)。因此，啟動至[!DNL LinkedIn Matched Audiences]的對象可能會被去除&#x200B;*雜湊*&#x200B;識別碼，例如電子郵件地址或行動裝置ID。

視您擷取至Adobe Experience Platform的ID類型而定，您必須遵守其對應要求。

## 電子郵件雜湊要求 {#email-hashing-requirements}

您可以在將電子郵件地址擷取至Adobe Experience Platform之前先雜湊電子郵件地址，或在Experience Platform中清楚使用電子郵件地址，並在啟用時讓[!DNL Platform]雜湊這些地址。

若要了解如何以Experience Platform擷取電子郵件地址，請參閱[批次擷取概述](/help/ingestion/batch-ingestion/overview.md)和[串流擷取概述](/help/ingestion/streaming-ingestion/overview.md)。

如果您選取自行雜湊電子郵件地址，請務必符合下列要求：

* 修剪電子郵件字串中的所有開頭和結尾空格。 例如：`johndoe@example.com`，而不是`<space>johndoe@example.com<space>`;
* 對電子郵件字串進行雜湊處理時，請務必將小寫字串雜湊；
   * 範例：`example@email.com`，而不是`EXAMPLE@EMAIL.COM`;
* 確認雜湊字串全部為小寫
   * 範例：`55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，而不是`55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* 別給繩子加鹽。

>[!NOTE]
>
>啟動後，[!DNL Platform]會自動雜湊來自未雜湊命名空間的資料。
> 屬性來源資料不會自動雜湊。
> 
> 在[身分對應](../../ui/activate-destinations.md#mapping)步驟中，當您的來源欄位包含未雜湊屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。
> 
> 只有在選擇屬性作為源欄位時，才會顯示&#x200B;**[!UICONTROL 應用轉換]**&#x200B;選項。 當您選擇命名空間時，不會顯示。

![身分對應轉換](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

以下影片也示範設定[!DNL LinkedIn Matched Audiences]目的地和啟用區段的步驟。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform使用者介面經常更新，且自此視訊錄制以來可能已變更。 有關最新資訊，請參閱[目標配置教程](../../ui/connect-destination.md)。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:您日後可據以識別此目的地的名稱。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:您的 [!DNL LinkedIn Campaign Manager Account ID]。您可以在[!DNL LinkedIn Campaign Manager]帳戶中找到此ID。

## 啟用此目的地的區段 {#activate}

請參閱[將設定檔和區段啟用至目的地](../../ui/activate-destinations.md) ，以取得將對象區段啟用至目的地的指示。

## 匯出的資料 {#exported-data}

成功啟動表示會以程式設計方式在[[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login)中建立[!DNL LinkedIn]自訂對象。 當使用者符合已啟動區段的資格或取消資格時，會新增及移除對象中的區段成員資格。

>[!TIP]
>
>Adobe Experience Platform與[!DNL LinkedIn Matched Audiences]之間的整合支援歷史受眾回填。 當您將區段啟用至目的地時，所有歷史區段資格都會傳送至[!DNL LinkedIn]。
