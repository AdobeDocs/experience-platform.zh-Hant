---
keywords: linkedin連線；linkedin連線；linkedin目的地；linkedin;
title: Linkedin相符的對象連線
description: 根據雜湊電子郵件，啟用LinkedIn行銷活動的設定檔，以鎖定對象、個人化和隱藏。
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 2%

---

# [!DNL LinkedIn Matched Audiences] 連接

## 總覽 {#overview}

為您的 [!DNL LinkedIn] 根據雜湊電子郵件和行動ID進行對象鎖定目標、個人化和隱藏的行銷活動。

![linkedInAdobe Experience Platform UI中的目的地](../../assets/catalog/social/linkedin/catalog.png)

## 使用案例

協助您更清楚了解如何及何時使用 [!DNL LinkedIn Matched Audiences] 目的地，以下是Adobe Experience Platform客戶可透過此功能解決的使用案例。

軟體公司組織會議，希望與參與者保持聯繫，並根據他們的會議出席情況向他們顯示個性化優惠。 公司可以從自己的網站擷取電子郵件地址或行動裝置ID [!DNL CRM] 進入Adobe Experience Platform。 接著，他們可以從自己的離線資料建立區段，並將這些區段傳送至 [!DNL LinkedIn] 社交平台，最佳化其廣告支出。

## 支援的身分 {#supported-identities}

[!DNL LinkedIn Matched Audiences] 支援啟用下表所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google Advertising ID | 當源標識為GAID命名空間時，選擇此目標標識。 |
| IDFA | Apple ID for Advertisers | 當您的來源識別為IDFA命名空間時，請選取此目標識別。 |
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 遵循 [ID比對需求](#id-matching-requirements-id-matching-requirements) 區段，並分別對純文字和雜湊電子郵件使用適當的命名空間。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。 |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，其中包含 [!DNL LinkedIn Matched Audiences] 目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## linkedIn帳戶必要條件 {#LinkedIn-account-prerequisites}

您可以使用 [!UICONTROL linkedIn相符的對象] 目的地，請確定 [!DNL LinkedIn Campaign Manager] 帳戶具有 [!DNL Creative Manager] 權限層級或更高。

了解如何編輯 [!DNL LinkedIn Campaign Manager] 使用者權限，請參閱 [新增、編輯及移除Advertising帳戶的使用者權限](https://www.linkedin.com/help/lms/answer/5753) 在LinkedIn檔案中。

## ID比對需求 {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] 需要清楚傳送任何個人識別資訊(PII)。 因此，對象已啟動至 [!DNL LinkedIn Matched Audiences] 可以砍掉 *雜湊* 識別碼，例如電子郵件地址或行動裝置ID。

視您擷取至Adobe Experience Platform的ID類型而定，您必須遵守其對應要求。

## 電子郵件雜湊要求 {#email-hashing-requirements}

您可以先雜湊電子郵件地址再將其擷取至Adobe Experience Platform，或在Experience Platform中清除使用電子郵件地址，並 [!DNL Platform] 激活時將其哈希。

若要了解如何在Experience Platform中擷取電子郵件地址，請參閱 [批次匯入概觀](/help/ingestion/batch-ingestion/overview.md) 和 [串流獲取概觀](/help/ingestion/streaming-ingestion/overview.md).

如果您選取自行雜湊電子郵件地址，請務必符合下列要求：

* 修剪電子郵件字串中的所有開頭和結尾空格。 例如： `johndoe@example.com`，而非 `<space>johndoe@example.com<space>`;
* 對電子郵件字串進行雜湊處理時，請務必將小寫字串雜湊；
   * 範例： `example@email.com`，而非 `EXAMPLE@EMAIL.COM`;
* 確認雜湊字串全部為小寫
   * 範例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，而非 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* 別給繩子加鹽。

>[!NOTE]
>
>來自未雜湊命名空間的資料會由 [!DNL Platform] 啟動後。
> 屬性來源資料不會自動雜湊。
> 
> 在 [身分對應](../../ui/activate-segment-streaming-destinations.md#mapping) 步驟，當您的來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。
> 
> 此 **[!UICONTROL 套用轉換]** 選擇「屬性」作為源欄位時，才會顯示「選項」。 當您選擇命名空間時，不會顯示。

![身分對應轉換](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

以下影片也示範設定 [!DNL LinkedIn Matched Audiences] 目的地和啟用區段。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform使用者介面經常更新，且自此視訊錄制以來可能已變更。 如需最新資訊，請參閱 [目的地設定教學課程](../../ui/connect-destination.md).

### 驗證到目標 {#authenticate}

1. 尋找 [!DNL LinkedIn Matched Audiences] 目標目錄中的目標，然後選取 **[!UICONTROL 設定]**.
2. 選擇 **[!UICONTROL 連接到目標]**.
   ![驗證LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. 輸入您的LinkedIn憑證並選取 **登入**.

### 填寫目的地詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="帳戶 ID"
>abstract="您的 LinkedIn 行銷活動管理員帳戶 ID。您可以在您的 LinkedIn 行銷活動管理員帳戶中找到此 ID。"

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:您的 [!DNL LinkedIn Campaign Manager Account ID]. 您可以在 [!DNL LinkedIn Campaign Manager] 帳戶。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 匯出的資料 {#exported-data}

成功啟動表示 [!DNL LinkedIn] 自訂對象會以程式設計方式建立於 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). 當使用者符合已啟動區段的資格或取消資格時，會新增及移除對象中的區段成員資格。

>[!TIP]
>
>Adobe Experience Platform與 [!DNL LinkedIn Matched Audiences] 支援歷史受眾回填。 所有歷史區段資格都會傳送至 [!DNL LinkedIn] 將區段啟用至目的地時。
