---
title: SAP Commerce連線
description: 使用SAP Commerce目標聯結器更新SAP帳戶中的客戶記錄。
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 3bd1a2a7-fb56-472d-b9bd-603b94a8937e
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '2175'
ht-degree: 3%

---

# [!DNL SAP Commerce] 連線

[!DNL SAP Commerce] （先前稱為[[!DNL Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html)）是適用於B2B和B2C企業的雲端型電子商務平台解決方案，可作為SAP客戶體驗產品組合的一部分提供。 [[!DNL SAP] 訂閱帳單](https://www.sap.com/products/financial-management/subscription-billing.html)是產品組合下的產品，可透過標準化的整合，透過簡化的銷售和付款體驗來啟用完整的訂閱生命週期管理。

此[!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md)使用[[!DNL SAP Subscription Billing] 客戶管理API](https://api.sap.com/api/BusinessPartner_APIs/path/PUT_customers-customerNumber)，在啟用後於[!DNL SAP Commerce]內從現有Experience Platform對象更新您的客戶詳細資料。

[!DNL SAP Commerce]向目的地驗證[區段中進一步說明如何向您的](#authenticate)執行個體進行驗證。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL SAP Commerce]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

[!DNL SAP Commerce]客戶會儲存與您業務互動的個人或組織實體的相關資訊。 您的團隊使用[!DNL SAP Commerce]中現有的客戶來建置Experience Platform對象。 將這些對象傳送到[!DNL SAP Commerce]後，其資訊會更新，並且會為每個客戶指派屬性，其值會作為對象名稱，指出客戶屬於哪個對象。

## 先決條件 {#prerequisites}

請參閱以下各節，瞭解您必須在Experience Platform和[!DNL SAP Commerce]中設定的任何先決條件，以及使用[!DNL SAP Commerce]目的地之前必須收集的資訊。

### Experience Platform必要條件 {#prerequisites-in-experience-platform}

在啟用資料至[!DNL SAP Commerce]目的地之前，您必須在[中建立](/help/xdm/schema/composition.md)結構描述[、](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)資料集[和](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html)對象[!DNL Experience Platform]。

如果您需要對象狀態的指引，請參閱[對象成員資格詳細資料結構描述欄位群組](/help/xdm/field-groups/profile/segmentation.md)的Experience Platform檔案。

### [!DNL SAP Commerce]目的地的先決條件 {#prerequisites-destination}

若要將資料從Experience Platform匯出至您的[!DNL SAP Commerce]帳戶，請注意下列必要條件：

#### 您必須擁有[!DNL SAP Subscription Billing]帳戶 {#prerequisites-account}

若要將資料從Experience Platform匯出至您的[!DNL SAP Commerce]帳戶，您需要有[!DNL SAP Subscription Billing]帳戶。 如果您沒有有效的帳單帳戶，請連絡您的[!DNL SAP]帳戶管理員。 如需其他詳細資訊，請參閱[[!DNL SAP] 平台組態](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf)檔案。

#### 產生服務金鑰 {#prerequisites-service-key}

* [!DNL SAP Commerce]服務金鑰可讓您透過Experience Platform存取[!DNL SAP Subscription Billing] API。 請參考[!DNL SAP Commerce] [使用使用者端ID和使用者端密碼](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/87c11a0f5dc3494eaf3baa355925c030.html#create-a-service-key-with-client-id-and-client-secret)建立服務金鑰，以建立服務金鑰。 [!DNL SAP Commerce] 需要下列項目:
   * 用戶端 ID
   * 用戶端密碼
   * URL。 URL模式如下： `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`。 此值稍後將用於取得`Region`和`Endpoint`的值。

+++選取以檢視服務金鑰的範例

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

#### 在[!DNL SAP Subscription Billing]中建立自訂參考 {#prerequisites-custom-reference}

若要在[!DNL SAP Subscription Billing]中更新Experience Platform對象狀態，您需要在Experience Platform中為每個選取的對象設定一個自訂參考欄位。

若要建立自訂參考，請登入您的[!DNL SAP Subscription Billing]帳戶，並導覽至&#x200B;**[主要資料和組態]** > **[自訂參考]**&#x200B;頁面。 接著，選取「**[!UICONTROL Create]**」，為Experience Platform中選取的每個對象新增參考。 在後續[排程對象匯出和範例](#schedule-segment-export-example)步驟中，您將需要這些參考欄位名稱。

以下顯示如何在&#x200B;**[!UICONTROL Reference Type]**&#x200B;內建立自訂[!DNL SAP Subscription Billing]的範例：
![顯示在SAP訂閱帳單中建立自訂參考的位置的影像。](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

如需其他指南，請參閱[!DNL SAP Subscription Billing] [自訂參考資料](https://help.sap.com/docs/CLOUD_TO_CASH_OD/80d121f216af43648e79664efe5595f7/85696a63c8d8453a934e86c9413a25cf.html?version=2023-11-27)檔案。

### 收集必要的認證 {#gather-credentials}

若要將[!DNL SAP Commerce]連線至Experience Platform，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| --- | --- |
| 用戶端 ID | 服務金鑰中的`clientId`值。 |
| 用戶端密碼 | 服務金鑰中的`clientSecret`值。 |
| 端點 | 服務機碼中的`url`值類似`https://subscriptionbilling.authentication.eu10.hana.ondemand.com`。 |
| 區域 | 您的資料中心位置。 區域出現在`url`中，其值類似於`eu10`或`us10`。 例如，如果`url`是`https://eu10.revenue.cloud.sap/api`，您需要`eu10`。 |

## 護欄 {#guardrails}

對[!DNL SAP Cloud Management service]的API要求受限於[速率限制](https://help.sap.com/docs/btp/sap-business-technology-platform/account-administration-rate-limiting)。 超過速率限制時，您會遇到`HTTP 429 Too Many Requests`回應狀態代碼。

## 支援的身分 {#supported-identities}

[!DNL SAP Commerce]支援下表中描述的身分更新。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
| --- | --- | --- |
| `customerNumberSAP` | 您[!DNL SAP Commerce]帳戶中已有個人或企業客戶的客戶識別碼。 | 強制 |

## 支援的對象 {#supported-audiences}

本節說明您可以匯出至此目的地的所有對象。

此目的地支援啟用所有透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。

此目的地也支援下表所述的對象啟用。

| 客群類型 | 支援 | 說明 |
| ------------- | --------- | ----------- |
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL Profile-based]** | <ul><li>您正在匯出對象的所有成員，以及所需的結構描述欄位&#x200B;*（例如：電子郵件地址、電話號碼、姓氏）* （根據您的欄位對應）。</li><li> 針對Experience Platform中每個選取的對象，相對應的[!DNL SAP Commerce]個其他屬性會從Experience Platform更新其對象狀態。</li></ul> |
| 匯出頻率 | **[!UICONTROL Streaming]** | <ul><li>串流目的地是「一律開啟」的API型連線。 當根據對象評估在Experience Platform中更新設定檔時，聯結器會將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。</li></ul> |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

在&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**&#x200B;內，搜尋[!DNL SAP Commerce]。 或者，您可以在&#x200B;**[!UICONTROL eCommerce]**&#x200B;類別下找到它。

### 驗證目標 {#authenticate}

填寫以下必填欄位。 如需任何指引，請參閱[產生服務金鑰](#prerequisites-service-key)區段。

| 欄位 | 說明 |
| --- | --- |
| **[!UICONTROL Client ID]** | 服務金鑰中的`clientId`值。 |
| **[!UICONTROL Client secret]** | 服務金鑰中的`clientSecret`值。 |
| **[!UICONTROL Endpoint]** | 服務機碼中的`url`值類似`https://subscriptionbilling.authentication.eu10.hana.ondemand.com`。 |
| **[!UICONTROL Region]** | 您的資料中心位置。 區域出現在`url`中，其值類似於`eu10`或`us10`。 例如，如果`url`是`https://eu10.revenue.cloud.sap/api`，您需要`eu10`。 |

若要驗證到目的地，請選取&#x200B;**[!UICONTROL Connect to destination]**。
![來自Experience Platform UI的影像，顯示如何驗證至目的地。](../../assets/catalog/ecommerce/sap-commerce/authenticate-destination.png)

如果提供的詳細資料有效，UI會顯示帶有綠色勾號的&#x200B;**[!UICONTROL Connected]**&#x200B;狀態。 然後您可以繼續下一步驟。

### 填寫目標詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。
![來自Experience Platform UI的影像，顯示驗證後要填寫的目的地詳細資料。](../../assets/catalog/ecommerce/sap-commerce/destination-details.png)

* **[!UICONTROL Name]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL Description]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL Type of Customer]**：根據您對象中的實體，選取&#x200B;***個人***&#x200B;或&#x200B;***公司***。 [!DNL SAP Subscription Billing] [結構描述](https://api.sap.com/api/BusinessPartner_APIs/schema)會根據對應至`customerType`屬性的這個選取專案切換必要欄位。 如果選取專案是&#x200B;***公司***，則會忽略個別客戶所需的強制對應，例如`firstName`和`lastName`，且`company`會成為強制對應，反之亦然。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應屬性和身分 {#map}

若要將對象資料從Adobe Experience Platform正確傳送至[!DNL SAP Commerce]目的地，您必須完成欄位對應步驟。 對應包括在Experience Platform帳戶中的Experience Data Model (XDM)結構描述欄位與來自目標目的地的對應對應專案之間建立連結。 若要將您的XDM欄位正確對應到[!DNL SAP Commerce]目的地欄位，請遵循下列步驟：

#### 對應`customerNumberSAP`身分

`customerNumberSAP`識別是這個目的地的必要對應。 請依照下列步驟進行對應：

1. 在&#x200B;**[!UICONTROL Mapping]**&#x200B;步驟中，選取&#x200B;**[!UICONTROL Add new mapping]**。 您現在可以在畫面上看到新的對應列。
   ![Experience Platform UI熒幕擷取畫面，強調顯示「新增對應」按鈕。](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. 在&#x200B;**[!UICONTROL Select source field]**&#x200B;視窗中選擇&#x200B;**[!UICONTROL Select identity namespace]**&#x200B;並選取`customerNumberSAP`。
   ![Experience Platform UI熒幕擷圖選取電子郵件作為來源屬性，以對應為身分。](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-identity.png)
1. 在&#x200B;**[!UICONTROL Select target field]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL Select identity namespace]**&#x200B;並選取`customerNumber`身分。
   ![Experience Platform UI熒幕擷圖選取電子郵件作為目標屬性，以對應為身分。](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-identity.png)

| 來源欄位 | 目標欄位 | 強制 |
| --- | --- | --- |
| `IdentityMap: customerNumberSAP` | `Identity: customerNumber` | 是 |

具有身分對應的範例如下所示：
![來自Experience Platform UI的影像，顯示customerNumber身分對應範例。](../../assets/catalog/ecommerce/sap-commerce/mapping-identities.png)

#### 對應屬性

若要在XDM設定檔結構描述與[!DNL SAP Subscription Billing]帳戶之間新增任何其他要更新的屬性，請重複下列步驟：

1. 在&#x200B;**[!UICONTROL Mapping]**&#x200B;步驟中，選取&#x200B;**[!UICONTROL Add new mapping]**。 您現在可以在畫面上看到新的對應列。
   ![Experience Platform UI熒幕擷取畫面，強調顯示「新增對應」按鈕。](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. 在&#x200B;**[!UICONTROL Select source field]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL Select attributes]**&#x200B;類別並選取XDM屬性。
   ![Experience Platform UI熒幕擷圖選取姓氏作為來源屬性。](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-attribute.png)
1. 在&#x200B;**[!UICONTROL Select target field]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL Select custom attributes]**&#x200B;類別，並從客戶[!DNL SAP Subscription Billing]結構描述[屬性清單中輸入](https://api.sap.com/api/BusinessPartner_APIs/schema)屬性的名稱。
   ![Experience Platform UI熒幕擷取畫面，其中lastName定義為target屬性。](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-attribute.png)

>[!IMPORTANT]
>
> 目標欄位名稱區分大小寫，且應符合[!DNL SAP Subscription Billing]屬性名稱。 唯一的例外是`country`，您應該改用`countryCode`。 [!DNL SAP Subscription Billing]支援alpha-2 (ISO 3166)國家/地區代碼。 值區分大小寫，且必須介於0到3個字元之間，因此請確定您所提供的內容與定義完全相同，否則您會遇到錯誤： `The country code {} does not exist`或`size must be between 0 and 3`。

#### 對應所選客戶型別的`mandatory`屬性

強制屬性對應取決於您選取的&#x200B;**[!UICONTROL Type of Customer]**。 若要對應必要屬性，請從下列選項中選取：

>[!BEGINTABS]

>[!TAB 個別客戶]

| 來源欄位 | 目標欄位 | 強制 |
| --- | --- | --- |
| `xdm: person.lastName` | `Attribute: lastName` | 是 |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | 是 |

>[!TAB 公司客戶]

| 來源欄位 | 目標欄位 | 強制 |
| --- | --- | --- |
| `xdm: b2b.companyName` | `Attribute: company` | 是 |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | 是 |

>[!ENDTABS]

#### 對應其他屬性

然後，您可以在XDM設定檔結構描述與客戶的[!DNL SAP Subscription Billing] [結構描述](https://api.sap.com/api/BusinessPartner_APIs/schema)屬性之間新增任何其他對應，如下所示：

>[!BEGINTABS]

>[!TAB 個別客戶]

| 來源欄位 | 目標欄位 | 強制 |
| --- | --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstName` | 無 |
| `xdm: workAddress.street1` | `Attribute: street` | 無 |
| `xdm: workAddress.city` | `Attribute: city` | 無 |

以下是客戶為個人的強制和選用屬性對應的範例：
![來自Experience Platform UI的影像，顯示具有必要和選用屬性對應的範例，其中客戶為個人。](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-individual.png)

>[!TAB 公司客戶]

| 來源欄位 | 目標欄位 | 強制 |
| --- | --- | --- |
| `xdm: workAddress.street1` | `Attribute: street` | 無 |
| `xdm: workAddress.city` | `Attribute: city` | 無 |

以下是客戶為公司的具有強制和選擇性屬性對應的範例：
![來自Experience Platform UI的影像，顯示具有強制和選擇性屬性對應的範例，其中客戶是企業使用者。](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-corporate.png)

>[!ENDTABS]

當您完成提供目的地連線的對應時，請選取&#x200B;**[!UICONTROL Next]**。

### 排程對象匯出和範例 {#schedule-segment-export-example}

執行[排程對象匯出](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling)步驟時，您必須手動將Experience Platform對象對應到[中的](#prerequisites-attribute)屬性[!DNL SAP Subscription Billing]。

以下顯示反白顯示[!DNL SAP Commerce] **[!UICONTROL Mapping ID]**&#x200B;位置的排程對象匯出步驟範例：
![來自Experience Platform的影像，顯示填入對應ID的排程對象匯出。](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export.png)

若要這麼做，請選取每個區段，然後在[!DNL SAP Subscription Billing] [!DNL SAP Commerce]目的地聯結器欄位中，輸入來自&#x200B;**[!UICONTROL Mapping ID]**&#x200B;的自訂參考名稱。 如需建立自訂參考的指引，請參閱[在 [!DNL SAP Subscription Billing]](#prerequisites-custom-reference)中建立自訂參考區段。

>[!IMPORTANT]
>
> 請勿使用自訂參考標籤作為值。
> &#x200B;>![影像指示您不應該使用自訂參考標籤值來對應。](../../assets/catalog/ecommerce/sap-commerce/custom-reference-dont-use-label-for-mapping.png)

例如，如果您選取的Experience Platform對象為`sap_audience1`，而您想要將其狀態更新為[!DNL SAP Subscription Billing]自訂參考`SAP_1`，請在[!DNL SAP_Commerce] **[!UICONTROL Mapping ID]**&#x200B;欄位中指定此值。

以下顯示來自&#x200B;**[!UICONTROL Reference Type]**&#x200B;的範例[!DNL SAP Subscription Billing]：
![顯示在SAP訂閱帳單中建立自訂參考的位置的影像。](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

以下是排程對象匯出步驟的範例，該步驟已選取對象並反白顯示其對應的[!DNL SAP Commerce] **[!UICONTROL Mapping ID]**：
![來自Experience Platform的影像，顯示填入對應ID的排程對象匯出。](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export-example.png)

如圖所示，**[!UICONTROL Mapping ID]**&#x200B;欄位中的值應完全符合[!DNL SAP Subscription Billing] **[!UICONTROL Reference Type]**&#x200B;值。

對每個已啟動的Experience Platform對象重複此章節。

根據上方顯示的影像，您已選取兩個對象，對應將會如下所示：

| [!DNL SAP Commerce]對象名稱 | [!DNL SAP Subscription Billing] **[!UICONTROL Reference Type]** | [!DNL SAP Commerce] **[!UICONTROL Mapping ID]**&#x200B;值 |
| --- | --- | --- |
| sap_audience1 | `SAP_1` | `SAP_1` |
| SAP對象2 | `SAP_2` | `SAP_2` |

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

登入[!DNL SAP Subscription Billing]帳戶，然後導覽至&#x200B;**[!UICONTROL Contacts]**&#x200B;頁面以檢查對象狀態。 清單可設定為顯示自訂參考的欄，並顯示對應的對象狀態。
![SAP訂閱帳單影像，顯示客戶概觀頁面，其欄標題顯示對象名稱和儲存格對象狀態](../../assets/catalog/ecommerce/sap-commerce/customer-overview.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。

## 錯誤與疑難排解 {#errors-and-troubleshooting}

請參閱[[!DNL SAP Subscription Billing] 錯誤型別](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/1a6a0dd6129c48e8b235190a1b5409fa.html)檔案頁面，以取得可能的錯誤型別及其回應代碼清單。

## 其他資源 {#additional-resources}

[!DNL SAP]檔案中的其他實用資訊如下：

* [內建SAP訂閱帳單](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/e4b8badf7d124026991e4ab6b57d2a33.html)

### Changelog

本節擷取此目的地聯結器的功能和重要檔案更新。

+++ 檢視變更記錄檔

| 發行月份 | 更新型別 | 說明 |
|---|---|---|
| 2024 年 1 月 | 首次發行 | 初始目的地版本和檔案發佈。 |

{style="table-layout:auto"}

+++
