---
keywords: crm；CRM；crm目的地；salesforce crm；salesforce crm目的地
title: Salesforce CRM連線
description: Salesforce CRM目的地可讓您匯出帳戶資料，並在Salesforce CRM中根據您的業務需求加以啟用。
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '2818'
ht-degree: 1%

---

# [!DNL Salesforce CRM] 連線

## 概觀 {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) 是熱門的客戶關係管理(CRM)平台，並支援底下所述的設定檔型別：

* [銷售機會](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm)  — 潛在客戶是可能對您銷售的產品或服務感興趣（或不感興趣）的個人或公司名稱。
* [連絡人](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm)  — 聯絡人是指您的代表已建立關係且已取得潛在客戶資格的個人。

這個 [!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md) 可運用 [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm)，可支援上述兩種設定檔型別。

時間 [啟用區段](#activate)，您可在潛在客戶或聯絡人之間選取，並將屬性和受眾資料更新至 [!DNL Salesforce CRM].

[!DNL Salesforce CRM] 使用具有密碼授予的OAuth 2作為驗證機制，與Salesforce REST API通訊。 向您的驗證指示 [!DNL Salesforce CRM] 執行個體的詳細資訊如下： [驗證到目的地](#authenticate) 區段。

## 使用案例 {#use-cases}

行銷人員可以根據使用者Adobe Experience Platform設定檔中的屬性，將個人化體驗提供給使用者。 您可以從您的離線資料建立受眾，並將這些受眾傳送至Salesforce CRM，以便在Adobe Experience Platform中更新受眾和設定檔後立即更新CRM會籍。

## 先決條件 {#prerequisites}

### Experience Platform的必要條件 {#prerequisites-in-experience-platform}

在啟用資料至Salesforce CRM目的地之前，您必須擁有 [綱要](/help/xdm/schema/composition.md)， a [資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)、和 [區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) 建立於 [!DNL Experience Platform].

### 中的必要條件 [!DNL Salesforce CRM] {#prerequisites-destination}

請注意中的下列必要條件 [!DNL Salesforce CRM]，將資料從Platform匯出至您的Salesforce帳戶：

#### 您需要擁有 [!DNL Salesforce] 帳戶 {#prerequisites-account}

前往 [!DNL Salesforce] [試用版](https://www.salesforce.com/in/form/signup/freetrial-sales/) 頁面以註冊及建立 [!DNL Salesforce] 帳戶（如果尚未擁有）。

#### 在中設定已連線的應用程式 [!DNL Salesforce] {#prerequisites-connected-app}

首先，您需要設定 [[!DNL Salesforce] 已連線的應用程式](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) 在您的 [!DNL Salesforce] 帳戶（如果尚未擁有）。 [!DNL Salesforce CRM] 將善用已連線的應用程式來連線至 [!DNL Salesforce].

下一步，啟用 [!DNL OAuth Settings for API Integration] 針對 [!DNL Salesforce connected app]. 請參閱 [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 指南檔案。

此外，請確保 [範圍](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) 已為「 」選取 [!DNL Salesforce connected app].

* ``chatter_api``
* ``lightning``
* ``visualforce``
* ``content``
* ``openid``
* ``full``
* ``api``
* ``web``
* ``refresh_token``
* ``offline_access``

最後，確認 `password` 授權已在您的網站中 [!DNL Salesforce] 帳戶。 請參閱 [!DNL Salesforce] [OAuth 2.0特殊案例的使用者名稱密碼流程](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) 說明檔案（若您需要指引）。

>[!IMPORTANT]
>
>若您的 [!DNL Salesforce] 帳戶管理員已限制受信任IP範圍的存取權，您需要聯絡他們以取得 [EXPERIENCE PLATFORMIP](/help/destinations/catalog/streaming/ip-address-allow-list.md) 加入允許清單。 請參閱 [!DNL Salesforce] [限制連線應用程式可信任的IP範圍存取權](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 說明檔案（若您需要其他指引）。

#### 在中建立自訂欄位 [!DNL Salesforce] {#prerequisites-custom-field}

將對象啟用至 [!DNL Salesforce CRM] 目的地，您必須在 **[!UICONTROL 對應ID]** 欄位中針對每個已啟用的對象， **[對象排程](#schedule-segment-export-example)** 步驟。

[!DNL Salesforce CRM] 需要此值才能正確讀取和解讀來自Experience Platform的受眾，並在中更新其受眾狀態 [!DNL Salesforce]. 請參閱Experience Platform檔案以瞭解 [對象成員資格詳細資料結構欄位群組](/help/xdm/field-groups/profile/segmentation.md) 如果您需要對象狀態的指引。

針對您從Platform啟用的每個對象，設定為 [!DNL Salesforce CRM]，您需要建立型別的自訂欄位 `Text Area (Long)` 範圍 [!DNL Salesforce]. 您可以根據業務需求，定義任何大小的欄位字元長度，範圍在256到131,072個字元之間。 請參閱 [!DNL Salesforce] [自訂欄位型別](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5) 說明檔案頁面，以取得自訂欄位型別的其他資訊。 另請參閱 [!DNL Salesforce] 檔案至 [建立自訂欄位](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) 若您需要欄位建立方面的協助。

>[!IMPORTANT]
>
>請勿在欄位名稱中包含空白字元。 請改用底線 `(_)` 分隔符號的字元。
>範圍 [!DNL Salesforce] 您必須使用建立自訂欄位 **[!UICONTROL 欄位名稱]** 完全符合中指定的值 **[!UICONTROL 對應ID]** 適用於每個已啟動的Platform區段。 例如，底下熒幕擷圖顯示自訂欄位： `crm_2_seg`. 將對象啟用至此目的地時，新增 `crm_2_seg` 作為 **[!UICONTROL 對應ID]** 從Experience Platform將對象填入此自訂欄位。

在中建立自訂欄位的範例 [!DNL Salesforce]， *步驟1 — 選取資料型別*，如下所示：
![Salesforce UI熒幕擷圖顯示自訂欄位建立，步驟1 — 選取資料型別。](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

在中建立自訂欄位的範例 [!DNL Salesforce]， *步驟2 — 輸入自訂欄位的詳細資料*，如下所示：
![Salesforce UI熒幕擷圖顯示自訂欄位建立，步驟2 — 輸入自訂欄位的詳細資料。](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* 區分用於Platform受眾的自訂欄位和中的其他自訂欄位 [!DNL Salesforce] 建立自訂欄位時，您可以包含可辨識的前置詞或後置詞。 例如，不使用 `test_segment`，使用 `Adobe_test_segment` 或 `test_segment_Adobe`
>* 如果您在中已建立其他自訂欄位 [!DNL Salesforce]，您可以使用與平台區段相同的名稱，輕鬆識別中的對象 [!DNL Salesforce].

>[!NOTE]
>
>* Salesforce中的物件限制在25個外部欄位，請參閱 [自訂欄位屬性](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* 此限制表示您在任何時間最多只能有25個作用中的Experience Platform對象會籍。
>* 如果您在Salesforce中達到此限制，則必須從用來針對Experience Platform中舊版對象儲存對象狀態的Salesforce中移除自訂屬性，然後再新增對象 **[!UICONTROL 對應ID]** 可使用。

#### 彙總 [!DNL Salesforce CRM] 認證 {#gather-credentials}

在驗證之前，請記下以下專案 [!DNL Salesforce CRM] 目的地：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| `Username` | 您的 [!DNL Salesforce] 帳戶使用者名稱。 | |
| `Password` | 您的 [!DNL Salesforce] 帳戶密碼。 | |
| `Security Token` | 您的 [!DNL Salesforce] 安全性權杖，您稍後會將其附加至您的結尾 [!DNL Salesforce] 用來建立串連字串的密碼，以用作 **[!UICONTROL 密碼]** 當 [正在向目的地進行驗證](#authenticate).<br> 請參閱 [!DNL Salesforce] 檔案至 [重設您的安全性權杖](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5) 以瞭解如何從重新產生 [!DNL Salesforce] 介面（如果您沒有安全性權杖）。 |  |
| `Custom Domain` | 您的 [!DNL Salesforce] 網域前置詞。 <br> 請參閱 [[!DNL Salesforce] 檔案](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) 以瞭解如何從取得此值 [!DNL Salesforce] 介面。 | 若您的 [!DNL Salesforce] 網域為<br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*，<br> 您將需要 `d5i000000isb4eak-dev-ed` 做為值。 |
| `Client ID` | 您的Salesforce `Consumer Key`. <br> 請參閱 [[!DNL Salesforce] 檔案](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 以瞭解如何從取得此值 [!DNL Salesforce] 介面。 | |
| `Client Secret` | 您的Salesforce `Consumer Secret`. <br> 請參閱 [[!DNL Salesforce] 檔案](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) 以瞭解如何從取得此值 [!DNL Salesforce] 介面。 | |

### 護欄 {#guardrails}

[!DNL Salesforce] 強制要求、速率和逾時限制，以平衡交易載入。 請參閱 [API要求限制和配置](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) 以取得詳細資訊。

若您的 [!DNL Salesforce] 帳戶管理員已強制執行IP限制，您必須新增 [Experience PlatformIP位址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 至您的 [!DNL Salesforce] 帳戶的受信任IP範圍。 請參閱 [!DNL Salesforce] [限制連線應用程式可信任的IP範圍存取權](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 說明檔案（若您需要其他指引）。

>[!IMPORTANT]
>
>時間 [啟用區段](#activate) 您必須選取 *連絡人* 或 *銷售機會* 型別。 您必須確保您的對象擁有根據所選型別的適當資料對應。

## 支援的身分 {#supported-identities}

[!DNL Salesforce CRM] 支援下表中描述的身分更新。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| `SalesforceId` | 此 [!DNL Salesforce CRM] 您透過區段匯出或更新之聯絡人或潛在客戶身分的識別碼。 | 強制 |

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | <ul><li>您正在匯出區段的所有成員，以及所需的結構欄位 *（例如：電子郵件地址、電話號碼、姓氏）*，根據您的欄位對應。</li><li> 中的每個對象狀態 [!DNL Salesforce CRM] 會根據 **[!UICONTROL 對應ID]** 值期間提供 [對象排程](#schedule-segment-export-example) 步驟。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | <ul><li>串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

範圍 **[!UICONTROL 目的地]** > **[!UICONTROL 目錄]** 搜尋 [!DNL Salesforce CRM]. 或者，您可以在 **[!UICONTROL CRM]** 類別。

### 驗證目標 {#authenticate}

若要向目的地進行驗證，請填寫以下必填欄位並選取 **[!UICONTROL 連線到目的地]**. 請參閱 [彙總 [!DNL Salesforce CRM] 認證](#gather-credentials) 區段以取得任何指引。
|認證 |說明 | | — | — | | **[!UICONTROL 使用者名稱]** |您的 [!DNL Salesforce] 帳戶使用者名稱。 | | **[!UICONTROL 密碼]** |由下列專案組成的串連字串 [!DNL Salesforce] 帳戶密碼已附加您的 [!DNL Salesforce] 安全性Token。<br>串連值採用以下形式 `{PASSWORD}{TOKEN}`.<br> 請注意，請勿使用任何大括弧或空格。<br>例如，若您的 [!DNL Salesforce] 密碼為 `MyPa$$w0rd123` 和 [!DNL Salesforce] 安全性權杖是 `TOKEN12345....0000`，即您在中使用的串連值 **[!UICONTROL 密碼]** 欄位為 `MyPa$$w0rd123TOKEN12345....0000`. | | **[!UICONTROL 自訂網域]** |您的 [!DNL Salesforce] 網域前置詞。 <br>例如，如果您的網域為 *`d5i000000isb4eak-dev-ed`.my.salesforce.com*，您必須提供 `d5i000000isb4eak-dev-ed` 做為值。 | | **[!UICONTROL 使用者端ID]** |您的 [!DNL Salesforce] 已連線的應用程式 `Consumer Key`. | | **[!UICONTROL 使用者端密碼]** |您的 [!DNL Salesforce] 已連線的應用程式 `Consumer Secret`. |

![顯示如何驗證的平台UI熒幕擷圖。](../../assets/catalog/crm/salesforce/authenticate-destination.png)

如果提供的詳細資料有效，UI會顯示 **[!UICONTROL 已連線]** 狀態，並顯示綠色核取記號，您就可以繼續進行下一個步驟。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。
* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Salesforce ID型別]**：
   * 選取 **[!UICONTROL 連絡人]** 如果您要匯出或更新身分屬於型別 *連絡人*.
   * 選取 **[!UICONTROL 銷售機會]** 如果您要匯出或更新身分屬於型別 *銷售機會*.

![顯示目的地詳細資訊的平台UI熒幕擷圖。](../../assets/catalog/crm/salesforce/destination-details.png)

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

讀取 [將設定檔和受眾啟用至串流受眾匯出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要正確將對象資料從Adobe Experience Platform傳送至 [!DNL Salesforce CRM] 目的地，您必須進行欄位對應步驟。 對應包括在Platform帳戶中的Experience Data Model (XDM)結構描述欄位與來自目標目的地的對應對應專案之間建立連結。

中指定的屬性 **[!UICONTROL 目標欄位]** 應完全依照屬性對應表格中的說明命名，因為這些屬性將構成請求內文。

中指定的屬性 **[!UICONTROL 來源欄位]** 請勿遵循任何這類限制。 您可以視需要加以對應，但請確定輸入資料的格式根據 [[!DNL Salesforce] 檔案](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5). 如果輸入資料無效，則更新呼叫 [!DNL Salesforce] 將會失敗，您的連絡人/潛在客戶將不會更新。

若要正確將XDM欄位對應至 [!DNL (API) Salesforce CRM] 目的地欄位，請遵循下列步驟：

1. 在 **[!UICONTROL 對應]** 步驟，選取 **[!UICONTROL 新增對應]**，您會在畫面上看到新的對應列。
   ![「新增對應」的平台UI熒幕擷圖範例。](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. 在 **[!UICONTROL 選取來源欄位]** 視窗，選擇 **[!UICONTROL 選取屬性]** 類別並選取XDM屬性或選擇 **[!UICONTROL 選取身分名稱空間]** 並選取身分。
1. 在 **[!UICONTROL 選取目標欄位]** 視窗，選擇 **[!UICONTROL 選取身分名稱空間]** 並選取身分或選擇 **[!UICONTROL 選取自訂屬性]** 類別並選取屬性，或使用 **[!UICONTROL 屬性名稱]** 欄位。 請參閱 [[!DNL Salesforce CRM] 檔案](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) 以取得支援屬性的指引。
   * 重複這些步驟，在您的XDM設定檔結構描述之間新增下列對應，並 [!DNL (API) Salesforce CRM]：

   **使用連絡人**

   * 如果您使用的是 *連絡人* 在區段內，請參閱Salesforce中的「物件參考」，以瞭解 [連絡人](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) 以定義要更新欄位的對應。
   * 您可以透過搜尋字詞來識別必填欄位 *必填*，如上述連結的欄位說明中所述。
   * 根據您要匯出或更新之欄位，在XDM設定檔結構描述與之間新增對應 [!DNL (API) Salesforce CRM]： |來源欄位|目標欄位|附註 | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. 連絡人的姓氏，最多80個字元。 |\
     |`xdm: person.name.firstName`|`Attribute: FirstName`|連絡人的名字，最多40個字元。 | |`xdm: personalEmail.address`|`Attribute: Email`|連絡人的電子郵件地址。 |

   * 以下顯示使用這些對應的範例：
     ![顯示Target對應的平台UI熒幕擷取畫面範例。](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **使用銷售機會**

   * 如果您使用的是 *銷售機會* 在區段內，請參閱Salesforce中的「物件參考」，以瞭解 [銷售機會](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) 以定義要更新欄位的對應。
   * 您可以透過搜尋字詞來識別必填欄位 *必填*，如上述連結的欄位說明中所述。
   * 根據您要匯出或更新之欄位，在XDM設定檔結構描述與之間新增對應 [!DNL (API) Salesforce CRM]： |來源欄位|目標欄位|附註 | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. 銷售機會的姓氏，最多80個字元。 |\
     |`xdm: b2b.companyName`|`Attribute: Company`| `Mandatory`. 潛在客戶的公司。 | |`xdm: personalEmail.address`|`Attribute: Email`|潛在客戶的電子郵件地址。 |

   * 以下顯示使用這些對應的範例：
     ![顯示Target對應的平台UI熒幕擷取畫面範例。](../../assets/catalog/crm/salesforce/mappings-leads.png)

當您完成提供目的地連線的對應時，請選取 **[!UICONTROL 下一個]**.

### 排程對象匯出和範例 {#schedule-segment-export-example}

執行 [排程對象匯出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 步驟您必須手動將從Platform啟用的對象對應到中其對應的自訂欄位 [!DNL Salesforce].

要執行此操作，請選取每個區段，然後輸入自訂欄位名稱 [!DNL Salesforce] 在 [!DNL Salesforce CRM] **[!UICONTROL 對應ID]** 欄位。 請參閱 [在中建立自訂欄位 [!DNL Salesforce]](#prerequisites-custom-field) 有關在中建立自訂欄位的指引和最佳作法的區段 [!DNL Salesforce].

例如，如果您的 [!DNL Salesforce] 自訂欄位為 `crm_2_seg`，請在 [!DNL Salesforce CRM] **[!UICONTROL 對應ID]** 從Experience Platform將對象填入此自訂欄位。

來自的自訂欄位範例 [!DNL Salesforce] 如下所示：
![[!DNL Salesforce] 顯示自訂欄位的UI熒幕擷圖。](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

指示位置的 [!DNL Salesforce CRM] **[!UICONTROL 對應ID]** 如下所示：
![顯示排程對象匯出的平台UI熒幕擷取畫面範例。](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

如上方所示 [!DNL Salesforce] **[!UICONTROL 欄位名稱]** 完全符合中指定的值 [!DNL Salesforce CRM] **[!UICONTROL 對應ID]**.

根據您的使用案例，所有已啟用的對象皆可對映至相同的 [!DNL Salesforce] 自訂欄位或變更為其他 **[!UICONTROL 欄位名稱]** 在 [!DNL Salesforce CRM]. 以上圖影像為基礎的典型範例可能是。
| [!DNL Salesforce CRM] 區段名稱 | [!DNL Salesforce] **[!UICONTROL 欄位名稱]** | [!DNL Salesforce CRM] **[!UICONTROL 對應ID]** | | — | — | — | | crm_1_seg | `crm_1_seg` | `crm_1_seg` | | crm_2_seg | `crm_2_seg` | `crm_2_seg` |

對每個已啟動的Platform區段重複此章節。

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 選取 **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]** 以導覽至目的地清單。
   ![顯示瀏覽目的地的平台UI熒幕擷圖。](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. 選取目的地並驗證狀態是否為 **[!UICONTROL 已啟用]**.
   ![顯示目的地資料流執行的平台UI熒幕擷取畫面。](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. 切換至 **[!UICONTROL 啟用資料]** 標籤，然後選取對象名稱。
   ![顯示目的地啟用資料的平台UI熒幕擷圖範例。](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. 監控對象摘要，並確保設定檔計數對應於在區段內建立的計數。
   ![顯示區段的平台UI熒幕擷圖範例。](../../assets/catalog/crm/salesforce/segment.png)

1. 最後，登入Salesforce網站並驗證對象的設定檔是否已新增或更新。

   **使用連絡人**

   * 如果您已選取 *連絡人* 在您的Platform區段中，導覽至 **[!DNL Apps]** > **[!DNL Contacts]** 頁面。
     ![Salesforce CRM熒幕擷圖顯示具有區段設定檔的「連絡人」頁面。](../../assets/catalog/crm/salesforce/contacts.png)

   * 選取 *連絡人* 並檢查欄位是否已更新。 您可以在中看到每個對象狀態 [!DNL Salesforce CRM] 已根據「 」更新Platform中的對應對象狀態 **[!UICONTROL 對應ID]** 值期間提供 [對象排程](#schedule-segment-export-example).
     ![Salesforce CRM熒幕擷取畫面顯示「聯絡詳細資訊」頁面，其中包含更新的對象狀態。](../../assets/catalog/crm/salesforce/contact-info.png)

   **使用銷售機會**

   * 如果您已選取 *銷售機會* 在您的Platform區段中，導覽至 **[!DNL Apps]** > **[!DNL Leads]** 頁面。
     ![Salesforce CRM熒幕擷取畫面顯示「銷售機會」頁面，其中包含區段中的設定檔。](../../assets/catalog/crm/salesforce/leads.png)

   * 選取 *銷售機會* 並檢查欄位是否已更新。 您可以在中看到每個對象狀態 [!DNL Salesforce CRM] 已根據「 」更新Platform中的對應對象狀態 **[!UICONTROL 對應ID]** 值期間提供 [對象排程](#schedule-segment-export-example).
     ![Salesforce CRM熒幕擷取畫面顯示「銷售機會詳細資訊」頁面，其中包含更新的對象狀態。](../../assets/catalog/crm/salesforce/lead-info.png)

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).

## 錯誤與疑難排解 {#errors-and-troubleshooting}

### 將事件推播到目的地時遇到未知錯誤 {#unknown-errors}

* 檢查資料流執行時，您可能會遇到下列錯誤訊息： `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![平台UI熒幕擷圖顯示錯誤。](../../assets/catalog/crm/salesforce/error.png)

   * 若要修正此錯誤，請確認 **[!UICONTROL 對應ID]** 您在啟動工作流程中提供的資料給 [!DNL Salesforce CRM] 目的地與您在中建立的自訂欄位型別的值完全相符 [!DNL Salesforce]. 請參閱 [在中建立自訂欄位 [!DNL Salesforce]](#prerequisites-custom-field) 區段以取得指引。

* 啟用區段時，您可能會收到錯誤訊息： `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * 若要修正此錯誤，請連絡您的 [!DNL Salesforce] 要新增的帳戶管理員 [Experience PlatformIP位址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 至您的 [!DNL Salesforce] 帳戶的受信任IP範圍。 請參閱 [!DNL Salesforce] [限制連線應用程式可信任的IP範圍存取權](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) 說明檔案（若您需要其他指引）。

## 其他資源 {#additional-resources}

其他實用資訊來自 [Salesforce開發人員入口網站](https://developer.salesforce.com/) 如下：
* [快速入門](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [建立記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [自訂建議對象](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [使用複合資源](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* 此目的地會利用 [更新插入多筆記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API而非 [更新插入單一記錄](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) API呼叫。