---
title: Zendesk連線
description: Zendesk目的地可讓您匯出帳戶資料，並在Zendesk中根據您的業務需求加以啟用。
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: e7fcbbf4-5d6c-4abb-96cb-ea5b67a88711
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 2%

---

# [!DNL Zendesk] 連線

[[!DNL Zendesk]](https://www.zendesk.com) 是客戶服務解決方案與銷售工具。

這個 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 可運用 [[!DNL Zendesk] 連絡人API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/)，至 **建立和更新身分** 在對象中作為聯絡人 [!DNL Zendesk].

[!DNL Zendesk] 使用持有人權杖作為驗證機制，以與 [!DNL Zendesk] 連絡人API。 向您的驗證指示 [!DNL Zendesk] 執行個體的詳細資訊如下： [驗證到目的地](#authenticate) 區段。

## 使用案例 {#use-cases}

多管道B2C平台的客戶服務部門想要確保其客戶獲得順暢的個人化體驗。 部門可以從他們自己的離線資料建立對象，以建立新的使用者設定檔或更新不同互動（例如購買、退貨等）的現有設定檔資訊 並從Adobe Experience Platform將這些對象傳送至 [!DNL Zendesk]. 將更新的資訊存取 [!DNL Zendesk] 確保客戶服務代理程式能立即取得客戶的最新資訊，以便更快速地回應和解決問題。

## 先決條件 {#prerequisites}

### Experience Platform必要條件 {#prerequisites-in-experience-platform}

在將資料啟用至 [!DNL Zendesk] 目的地，您必須擁有 [綱要](/help/xdm/schema/composition.md)， a [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)、和 [區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) 建立於 [!DNL Experience Platform].

請參閱Experience Platform檔案，以瞭解 [對象成員資格詳細資料結構欄位群組](/help/xdm/field-groups/profile/segmentation.md) 如果您需要對象狀態的指引。

### [!DNL Zendesk] 必備條件 {#prerequisites-destination}

為了將資料從Platform匯出至 [!DNL Zendesk] 您需要擁有 [!DNL Zendesk] 帳戶。

#### 彙總 [!DNL Zendesk] 認證 {#gather-credentials}

在驗證之前，請記下以下專案 [!DNL Zendesk] 目的地：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| `Bearer token` | 您已在中產生的存取Token [!DNL Zendesk] 帳戶。 <br> 請依照檔案說明進行 [產生 [!DNL Zendesk] 存取權杖](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) 如果您沒有。 | `a0b1c2d3e4...v20w21x22y23z` |

## 護欄 {#guardrails}

此 [訂價與費率限制](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) 頁面詳細資訊 [!DNL Zendesk] 與您的帳戶相關聯的API限制。 您必須確保資料與承載皆符合這些限制。

## 支援的身分 {#supported-identities}

[!DNL Zendesk] 支援下表中描述的身分更新。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 範例 | 說明 | 強制 |
|---|---|---|---|
| `email` | `test@test.com` | 連絡人的電子郵件地址。 | 是 |

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | <ul><li>您正在匯出區段的所有成員，以及所需的結構欄位 *（例如：電子郵件地址、電話號碼、姓氏）*，根據您的欄位對應。</li><li> 中的每個區段狀態 [!DNL Zendesk] 會根據 **[!UICONTROL 對應ID]** 值期間提供 [對象排程](#schedule-segment-export-example) 步驟。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | <ul><li>串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

範圍 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]** 搜尋 [!DNL Zendesk]. 或者，您可以在 **[!UICONTROL CRM]** 類別。

### 驗證目標 {#authenticate}

填寫以下必填欄位。 請參閱 [彙總 [!DNL Zendesk] 認證](#gather-credentials) 區段以取得任何指引。
* **[!UICONTROL 持有人權杖]**：您在中產生的存取Token。 [!DNL Zendesk] 帳戶。

若要驗證目的地，請選取 **[!UICONTROL 連線到目的地]**.
![顯示如何驗證的平台UI熒幕擷圖。](../../assets/catalog/crm/zendesk/authenticate-destination.png)

如果提供的詳細資料有效，UI會顯示 **[!UICONTROL 已連線]** 帶有綠色勾號的狀態。 然後您可以繼續下一步驟。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。
![顯示目的地詳細資訊的平台UI熒幕擷圖。](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

讀取 [將設定檔和受眾啟用至串流受眾匯出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要正確將對象資料從Adobe Experience Platform傳送至 [!DNL Zendesk] 目的地，您必須進行欄位對應步驟。 對應包括在Platform帳戶中的Experience Data Model (XDM)結構描述欄位與來自目標目的地的對應對應專案之間建立連結。

中指定的屬性 **[!UICONTROL 目標欄位]** 應完全依照屬性對應表格中的說明命名，因為這些屬性將構成請求內文。

中指定的屬性 **[!UICONTROL 來源欄位]** 請勿遵循任何這類限制。 您可以視需要加以對應，但如果推送至時的資料格式不正確 [!DNL Zendesk] 這會導致錯誤。

若要正確將XDM欄位對應至 [!DNL Zendesk] 目的地欄位，請遵循下列步驟：

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**. 您會在畫面上看到新的對應列。
1. 在 **[!UICONTROL 選取來源欄位]** 視窗，選擇 **[!UICONTROL 選取屬性]** 類別並選取XDM屬性或選擇 **[!UICONTROL 選取身分名稱空間]** 並選取身分。
1. 在 **[!UICONTROL 選取目標欄位]** 視窗，選擇 **[!UICONTROL 選取身分名稱空間]** 類別並選取目標身分，或選擇 **[!UICONTROL 選取屬性]** 類別並選取其中一個支援的結構描述屬性。
   * 重複這些步驟以新增以下強制對應，您也可以在XDM設定檔結構描述與 [!DNL Zendesk] 例項： |來源欄位|目標欄位| 必填| |—|—|—| |`xdm: person.name.lastName`|`xdm: last_name`| 是 | |`IdentityMap: Email`|`Identity: email`| 是 | |`xdm: person.name.firstName`|`xdm: first_name`| |

   * 以下顯示使用這些對應的範例：
     ![具有屬性對應的平台UI熒幕擷圖範例。](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>此 `Attribute: last_name` 和 `Identity: email` 目標對應是此目的地的必要專案。 如果缺少這些對應，則會忽略任何其他對應且不會傳送至 [!DNL Zendesk].

完成提供目的地連線的對應後，選取 **[!UICONTROL 下一個]**.

### 排程對象匯出和範例 {#schedule-segment-export-example}

在 [[!UICONTROL 排程對象匯出]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 啟動工作流程的步驟，您必須手動將Platform對象對應至中的自訂欄位屬性 [!DNL Zendesk].

若要這麼做，請選取每個區段，然後輸入對應的自訂欄位屬性，從 [!DNL Zendesk] 在 **[!UICONTROL 對應ID]** 欄位。

範例如下：
![顯示排程對象匯出的平台UI熒幕擷取畫面範例。](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 選取 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** 並導覽至目的地清單。
1. 接下來，選取目的地並切換至 **[!UICONTROL 啟用資料]** 標籤，然後選取對象名稱。
   ![顯示目的地啟用資料的平台UI熒幕擷圖範例。](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. 監控對象摘要，並確保設定檔計數與區段中的計數相對應。
   ![顯示區段的平台UI熒幕擷圖範例。](../../assets/catalog/crm/zendesk/segment.png)

1. 登入 [!DNL Zendesk] 網站，然後導覽至 **[!UICONTROL 連絡人]** 頁面以檢查是否已新增對象中的設定檔。 此清單可設定為顯示與受眾建立之其他欄位的欄**[!UICONTROL 對應ID]使**者和受眾狀態。
   ![Zendesk UI熒幕擷圖顯示「連絡人」頁面，其中包含以對象名稱建立的其他欄位。](../../assets/catalog/crm/zendesk/contacts.png)

1. 或者，您可以向下展開至個人 **[!UICONTROL 個人]** 頁面，並檢查 **[!UICONTROL 其他欄位]** 顯示對象名稱和對象狀態的區段。
   ![Zendesk UI熒幕擷圖顯示「人員」頁面，而其他欄位區段顯示對象名稱和對象狀態。](../../assets/catalog/crm/zendesk/contact.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).

## 其他資源 {#additional-resources}

其他實用資訊來自 [!DNL Zendesk] 檔案如下：
* [撥打您的第一個電話](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [自訂欄位](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Changelog

本節擷取此目的地聯結器的功能和重要檔案更新。

+++ 檢視變更記錄檔

| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2023 年 4 月 | 檔案更新 | <ul><li>我們已更新 [使用案例](#use-cases) 區段，以更清楚的範例說明客戶何時可受益於使用此目的地。</li> <li>我們已更新 [對應](#mapping-considerations-example) 區段來反映正確的必要對應。 此 `Attribute: last_name` 和 `Identity: email` 目標對應是此目的地的必要專案。 如果缺少這些對應，則會忽略任何其他對應且不會傳送至 [!DNL Zendesk].</li> <li>我們已更新 [對應](#mapping-considerations-example) 區段，並提供強制和選用對應的清楚範例。</li></ul> |
| 2023 年 3 月 | 首次發行 | 初始目的地版本和檔案發佈。 |

{style="table-layout:auto"}

+++
