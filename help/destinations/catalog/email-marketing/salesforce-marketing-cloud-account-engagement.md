---
title: SalesforceMarketing Cloud帳戶參與
description: 了解如何使用SalesforceMarketing Cloud帳戶參與（先前稱為Pardot）目的地，匯出帳戶資料，並在SalesforceMarketing Cloud帳戶參與中根據您的業務需求啟用它。
last-substantial-update: 2023-04-14T00:00:00Z
source-git-commit: 65feb905bfa7d663d1d463d94af428a04dc55b01
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] 連接

使用 [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(先前稱為 [!DNL Pardot])* 目標，以擷取、追蹤、分數和等級銷售機會。 您也可以透過電子郵件滴漏式行銷活動和銷售機會管理，透過培養、評分和行銷活動細分，為目標市場區段和客戶群設計管道所有階段的銷售機會追蹤。

與 [!DNL Salesforce Marketing Cloud Engagement] 更注重 **B2C** 行銷， [!DNL Marketing Cloud Account Engagement] 最適合 **B2B** 涉及多個部門和決策者的使用案例，這些部門和決策者需要更長的銷售和決策週期。 此外，您也可以與CRM保持更接近和整合，以做出適當的銷售和行銷決策。 *注意，Experience Platform也有 [!DNL Salesforce Marketing Cloud Engagement]，您可以在 [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) 和 [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) 頁面。*

此 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 利用 [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email) 端點，到 **添加或更新銷售線索** 在新的 [!DNL Marketing Cloud Account Engagement] 區段。

[!DNL Marketing Cloud Account Engagement] 使用OAuth 2搭配授權碼通訊協定，對 [!DNL Account Engagement] API。 向您的 [!DNL Marketing Cloud Account Engagement] 執行個體在下方， [驗證到目標](#authenticate) 區段。

## 使用案例 {#use-cases}

以協助您更清楚了解應如何及何時使用 [!DNL Marketing Cloud Account Engagement] 目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。

### 傳送電子郵件給行銷活動的聯絡人 {#use-case-send-emails}

線上平台的行銷部門想要向B2B銷售機會的策展對象廣播電子郵件式行銷活動。 平台的行銷團隊可以透過Adobe Experience Platform新增銷售機會或更新現有銷售機會資訊、從自己的離線資料建立區段，並將這些區段傳送至 [!DNL Marketing Cloud Account Engagement]，然後可用來傳送行銷活動電子郵件。

## 先決條件 {#prerequisites}

如需在Experience Platform和 [!DNL Salesforce] 以及您在使用 [!DNL Marketing Cloud Account Engagement] 目的地。

### Experience Platform的必要條件 {#prerequisites-in-experience-platform}

在將資料啟用至 [!DNL Marketing Cloud Account Engagement] 目的地，您必須 [綱要](/help/xdm/schema/composition.md), [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)，和 [區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立於 [!DNL Experience Platform].

### 中的必要條件 [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

若要將資料從Platform匯出至您的 [!DNL Marketing Cloud Account Engagement] 帳戶：

#### 你需要 [!DNL Marketing Cloud Account Engagement] 帳戶 {#prerequisites-account}

A [!DNL Marketing Cloud Account Engagement] 具有訂閱的帳戶 [Marketing Cloud帳戶參與](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) 產品必須繼續。

您的 [!DNL Salesforce] 帳戶應具有 [!DNL Salesforce] `Account Engagement Administrator role`. 這是 [建立自定義潛在客戶欄位](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

最後，您的帳戶也應能存取 [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

伸手 [[!DNL Salesforce] 支援](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) 或 [!DNL Salesforce] 帳戶管理員（如果您沒有帳戶，或帳戶缺少） [!DNL Marketing Cloud Account Engagement] 訂閱或 [!DNL Account Engagement Administrator role].

#### 收集 [!DNL Marketing Cloud Account Engagement] 憑據 {#gather-credentials}

在驗證之前，請記下下列項目 [!DNL Marketing Cloud Account Engagement] 目的地。

| 憑據 | 說明 |
| --- | --- |
| `Username` | 您的 [!DNL Marketing Cloud Account Engagement] 帳戶使用者名稱。 |
| `Password` | 您的 [!DNL Marketing Cloud Account Engagement] 帳戶密碼。 |
| `Account Engagement Business Unit ID` | 要查找帳戶參與業務單元ID，請使用 [!DNL Salesforce]. 在設定中，輸入 *業務單元設定* 框中輸入URL。 您的帳戶參與業務單位ID開頭為 `0Uv` 長度為18個字元。 如果您無法訪問業務單元設定資訊，請詢問 [!DNL Salesforce] 帳戶管理員可提供 `Account Engagement Business Unit ID`. 若需要任何其他指引，請參閱 [[!DNL Salesforce] 驗證](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication) 指引頁面。 |

{style="table-layout:auto"}

### 護欄 {#guardrails}

請參閱 [!DNL Marketing Cloud Account Engagement] [比率限制](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) 詳細說明您的計畫所施加的限制，並將適用於Experience Platform執行。

>[!IMPORTANT]
>
>若您的 [!DNL Salesforce] 帳戶管理員對受信任IP範圍的存取權限受限，您需要聯絡這些範圍才能取得 [Experience PlatformIP](/help/destinations/catalog/streaming/ip-address-allow-list.md) 允許清單。 請參閱 [!DNL Salesforce] [限制對已連線應用程式的受信任IP範圍的存取](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 說明檔案。

## 支援的身分 {#supported-identities}

[!DNL Marketing Cloud Account Engagement] 支援啟用下表所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 潛在客戶電子郵件地址 | 必要 |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | <ul><li>您要匯出區段的所有成員，以及所需的結構欄位 *(例如：電子郵件地址、電話號碼、姓氏)*，根據您的欄位對應。</li><li> 對於Platform中的每個選取區段， [!DNL Salesforce Marketing Cloud Account Engagement] 區段狀態會從Platform更新，並顯示其區段狀態。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

內 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**，搜尋 [!DNL Salesforce Marketing Cloud Account Engagement]. 或者，您也可以在 **[!UICONTROL 電子郵件行銷]** 類別。

### 驗證到目標 {#authenticate}

要驗證到目標，請選擇 **[!UICONTROL 連接到目標]**. 系統會導覽至 [!DNL Salesforce] 登入頁面。 輸入 [!DNL Marketing Cloud Account Engagement] 帳戶憑證和選取 [!DNL Log In].

![Platform UI螢幕擷取畫面，顯示如何驗證以Marketing Cloud帳戶參與。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

下一步，選擇 [!UICONTROL 允許] 在後續視窗中為 **Adobe Experience Platform** 應用程式存取 [!DNL Salesforce Marketing Cloud Account Engagement] 帳戶。 *您只需執行一次*.

![Salesforce應用程式螢幕擷取確認快顯功能表，提供Experience Platform應用程式存取Marketing Cloud帳戶參與的權限。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

如果提供的詳細資料有效，UI會顯示訊息： *您已成功連接到SalesforceMarketing Cloud帳戶參與帳戶* 訊息與 **[!UICONTROL 已連接]** 狀態（加上綠色勾號），您就可以繼續進行下一個步驟。

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。 請參閱 [收集 [!DNL Marketing Cloud Account Engagement] 憑據](#gather-credentials) 區段。

![Platform UI螢幕擷取畫面，顯示目的地詳細資訊。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| 欄位 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 日後您將透過此名稱識別此目的地。 |
| **[!UICONTROL 說明]** | 未來可協助您識別此目的地的說明。 |
| **[!UICONTROL 帳戶參與業務單元ID]** | 您的 [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將您的對象資料從Adobe Experience Platform正確傳送至 [!DNL Marketing Cloud Account Engagement] 目的地，您必須執行欄位對應步驟。 對應包含在您的Platform帳戶中的Experience Data Model(XDM)結構欄位與目標目的地對應的欄位之間建立連結。

若要正確將XDM欄位對應至 [!DNL Marketing Cloud Account Engagement] 目標欄位，請遵循下列步驟。

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**. 畫面上會顯示新的對應列。
1. 在 **[!UICONTROL 選擇源欄位]** 窗口，選擇 **[!UICONTROL 選擇屬性]** 類別，然後選取XDM屬性或選擇 **[!UICONTROL 選取身分命名空間]** 並選擇身份。
1. 在 **[!UICONTROL 選擇目標欄位]** 窗口，選擇 **[!UICONTROL 選取身分命名空間]** 並選擇身份或 **[!UICONTROL 選取自訂屬性]** 類別，並從 [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) 從可用結構。

   * 重複這些步驟，新增XDM設定檔架構與 [!DNL Marketing Cloud Account Engagement]: |源欄位 |目標欄位 |必填 | | — | — | — | |`IdentityMap: Email`|`Identity: email`|是 | |`xdm: MailingAddress.city`|`xdm: city`| | |`xdm: person.name.firstName`|`Attribute: firstName`| |

   * 以下是具有上述對應的範例：
      ![Platform UI螢幕擷取範例，顯示Target對應。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

完成目標連接的映射後，請選擇 **[!UICONTROL 下一個]**.

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 導覽至您選取的其中一個區段。 選取 **[!DNL Activation data]** 索引標籤。此 **[!UICONTROL 對應ID]** 欄會顯示在 [!DNL Marketing Cloud Account Engagement Prospects] 頁面。
   ![Platform UI螢幕擷取範例，顯示所選區段的對應ID。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. 登入 [[!DNL Salesforce]](https://login.salesforce.com/) 網站。 然後導覽至 **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** 頁面，檢查區段中的潛在客戶是否已新增/更新。 或者，您也可以 [[!DNL Salesforce Pardot]](https://pi.pardot.com/) 並存取 **[!DNL Prospects]** 頁面。
   ![Salesforce UI螢幕截圖顯示Prospects頁面。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. 要檢查潛在客戶是否已更新，請選擇一個潛在客戶並驗證自定義潛在客戶欄位是否已以Experience Platform段狀態更新。
   ![Salesforce UI螢幕截圖顯示所選潛在客戶頁面，自訂潛在客戶欄位會以區段狀態更新。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).

## 其他資源 {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API檔案](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).