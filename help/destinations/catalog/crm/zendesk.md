---
title: Zendesk連接
description: Zendesk目的地允許您導出帳戶資料，並在Zendesk中激活它以滿足您的業務需要。
source-git-commit: 6a54926e47fb2364475dbf71593de97b642163d5
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 1%

---

# [!DNL Zendesk] 連接

[[!DNL Zendesk]](https://www.zendesk.com) 是客戶服務解決方案和銷售工具。

此 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 利用 [[!DNL Zendesk] 聯絡人API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/)，以在區段內建立和更新身分識別，做為內的聯絡人 [!DNL Zendesk].

[!DNL Zendesk] 使用承載令牌作為與通信的驗證機制 [!DNL Zendesk] 聯繫人API。 向您的 [!DNL Zendesk] 執行個體在下方， [驗證到目標](#authenticate) 區段。

## 使用案例 {#use-cases}

身為行銷人員，您可以根據使用者Adobe Experience Platform設定檔的屬性，為使用者提供個人化體驗。 您可以從離線資料建立區段，並將這些區段傳送至 [!DNL Zendesk]，可在Adobe Experience Platform中更新區段和設定檔時，立即顯示在使用者的動態消息中。

## 先決條件 {#prerequisites}

### Experience Platform必要條件 {#prerequisites-in-experience-platform}

在將資料啟用至 [!DNL Zendesk] 目的地，您必須 [綱要](/help/xdm/schema/composition.md), [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)，和 [區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 建立於 [!DNL Experience Platform].

請參閱的Experience Platform檔案 [區段成員資格詳細資料結構欄位群組](/help/xdm/field-groups/profile/segmentation.md) 如果您需要區段狀態的指引。

### [!DNL Zendesk] 必要條件 {#prerequisites-destination}

若要將資料從Platform匯出至 [!DNL Zendesk] 帳戶 [!DNL Zendesk] 帳戶。

#### 收集 [!DNL Zendesk] 憑據 {#gather-credentials}

在驗證之前，請記下下列項目 [!DNL Zendesk] 目的地：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `Bearer token` | 您在 [!DNL Zendesk] 帳戶。 <br> 請依照本檔案，前往 [產生 [!DNL Zendesk] 存取權杖](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) 如果你沒有。 | `a0b1c2d3e4...v20w21x22y23z` |

## 護欄 {#guardrails}

此 [定價和費率限制](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) 頁面詳細資訊 [!DNL Zendesk] 與您的帳戶相關聯的API限制。 您必須確定您的資料和裝載符合這些限制。

## 支援的身分 {#supported-identities}

[!DNL Zendesk] 支援下表所述的身分識別更新。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 範例 | 說明 | 必要 |
|---|---|---|---|
| `email` | `test@test.com` | 連絡人的電子郵件地址。 | 是 |

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | <ul><li>您要匯出區段的所有成員，以及所需的結構欄位 *(例如：電子郵件地址、電話號碼、姓氏)*，根據您的欄位對應。</li><li> 中的每個區段狀態 [!DNL Zendesk] 會根據 **[!UICONTROL 對應ID]** 值 [區段排程](#schedule-segment-export-example) 步驟。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | <ul><li>串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

內 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]** 搜尋 [!DNL Zendesk]. 或者，您也可以在 **[!UICONTROL CRM]** 類別。

### 驗證到目標 {#authenticate}

填寫下方的必填欄位。 請參閱 [收集 [!DNL Zendesk] 憑據](#gather-credentials) 區段。
* **[!UICONTROL 承載令牌]**:您在 [!DNL Zendesk] 帳戶。

要驗證到目標，請選擇 **[!UICONTROL 連接到目標]**.
![Platform UI螢幕擷取畫面，顯示如何驗證。](../../assets/catalog/crm/zendesk/authenticate-destination.png)

如果提供的詳細資料有效，UI會顯示 **[!UICONTROL 已連接]** 狀態（帶綠色複選標籤）。 接著，您可以繼續進行下一個步驟。

### 填寫目的地詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。
![Platform UI螢幕擷取畫面，顯示目的地詳細資訊。](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
>
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將您的對象資料從Adobe Experience Platform正確傳送至 [!DNL Zendesk] 目的地，您必須執行欄位對應步驟。 對應包含在您的Platform帳戶中的Experience Data Model(XDM)結構欄位與目標目的地對應的欄位之間建立連結。

在 **[!UICONTROL 目標欄位]** 名稱應與屬性對應表格中所述完全相同，因為這些屬性將構成請求內文。

在 **[!UICONTROL 源欄位]** 不遵守任何此類限制。 您可以視需要對應，但如果資料格式推送至時不正確 [!DNL Zendesk] 這會導致錯誤。

若要正確將XDM欄位對應至 [!DNL Zendesk] 目標欄位，請遵循下列步驟：

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**. 畫面上會顯示新的對應列。
1. 在 **[!UICONTROL 選擇源欄位]** 窗口，選擇 **[!UICONTROL 選擇屬性]** 類別，然後選取XDM屬性或選擇 **[!UICONTROL 選取身分命名空間]** 並選擇身份。
1. 在 **[!UICONTROL 選擇目標欄位]** 窗口，選擇 **[!UICONTROL 選取身分命名空間]** 並選擇身份或 **[!UICONTROL 選取自訂屬性]** 類別，並視需要選取屬性。
   * 重複這些步驟，新增XDM設定檔架構與 [!DNL Zendesk] 例項： |源欄位|目標欄位|必填| |—|—|—| |`xdm: person.name.lastName`|`Attribute: last_name` <br>或 `Attribute: name`|是 | |`IdentityMap: Email`|`Identity: email`|是 |

   * 使用這些對應的範例如下所示：
      ![Platform UI螢幕擷取範例及屬性對應。](../../assets/catalog/crm/zendesk/mappings.png)

      >[!IMPORTANT]
      >
      >目標欄位對應都是必填的，且是 [!DNL Zendesk] 工作。
      >
      >的對應 *姓氏* 或 *名稱* 為必要項目，否則 [!DNL Zendesk] API不會回應任何錯誤，且會忽略任何傳遞的屬性值。

完成為目標連接提供映射時，請選擇 **[!UICONTROL 下一個]**.

### 排程區段匯出和範例 {#schedule-segment-export-example}

在 [[!UICONTROL 排程區段匯出]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 在啟動工作流程的步驟中，您必須手動將Platform區段對應至 [!DNL Zendesk].

若要這麼做，請選取每個區段，然後輸入 [!DNL Zendesk] 在 **[!UICONTROL 對應ID]** 欄位。

以下是範例：
![Platform UI螢幕擷取範例，顯示「排程區段」匯出。](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 選擇 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** 並導覽至目的地清單。
1. 接下來，選取目的地並切換至 **[!UICONTROL 啟動資料]** ，然後選取區段名稱。
   ![Platform UI螢幕擷取範例，顯示「目的地啟動資料」。](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. 監控區段摘要，並確保設定檔的計數與區段內的計數相對應。
   ![Platform UI螢幕擷取範例，顯示「區段」。](../../assets/catalog/crm/zendesk/segment.png)

1. 登入 [!DNL Zendesk] 網站，然後導覽至 **[!UICONTROL 聯繫人]** 頁面，檢查區段中的設定檔是否已新增。 此清單可設定為顯示以區段建立之其他欄位的欄 **[!UICONTROL 對應ID]** 和區段狀態。
   ![Zendesk UI螢幕截圖顯示「聯繫人」頁，其中包含以段名稱建立的其他欄位。](../../assets/catalog/crm/zendesk/contacts.png)

1. 或者，您也可以深入鑽研個別 **[!UICONTROL 人員]** 頁面並檢查 **[!UICONTROL 其他欄位]** 區段來顯示區段名稱和區段狀態。
   ![Zendesk UI螢幕截圖顯示「人員」頁，其中包含顯示段名稱和段狀態的其他欄位部分。](../../assets/catalog/crm/zendesk/contact.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).

## 其他資源 {#additional-resources}

來自 [!DNL Zendesk] 檔案如下：
* [第一次打電話](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [自訂欄位](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)