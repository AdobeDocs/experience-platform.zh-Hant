---
title: (V1) Pega CDH即時受眾連線
description: 在Adobe Experience Platform中使用Pega客戶決定中心即時對象目的地，將設定檔屬性和對象成員資格資料傳送至Pega客戶決定中心，以做出次優決策。
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: 71de5b0d3e9c4413caa911fbe174e74c0e409d89
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 3%

---

# Pega CDH即時對象連線

>[!IMPORTANT]
>
>此版本的Pega客戶決定中心即時對象目的地僅支援單一Pega客戶決定應用程式。 如果您已設定多個Pega Customer Decision Hub應用程式，則需要使用[(V2) Pega CDH即時對象目的地聯結器](./pega-v2.md)。

## 概觀 {#overview}

使用Adobe Experience Platform中的[!DNL Pega Customer Decision Hub]即時對象目的地，將設定檔屬性和對象成員資格資料傳送至[!DNL Pega Customer Decision Hub]，以做出下一個最佳動作決策。

來自Adobe Experience Platform的設定檔對象成員資格，載入到[!DNL Pega Customer Decision Hub]中時，可用作最適化模型中的預測因子，並幫助提供正確的情境和行為資料，以實現次優行動決策。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由Pegasystems建立和維護的。 若有任何查詢或更新要求，請直接連絡Pega [這裡](mailto:support@pega.com)。

## 使用案例

為協助您更清楚瞭解您應如何及何時使用[!DNL Customer Decision Hub]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 電信

行銷人員想要運用[!DNL Pega Customer Decision Hub]提供的資料科學模型型次佳動作的深入分析，以吸引客戶參與。 [!DNL Pega Customer Decision Hub]非常依賴客戶意圖，例如「Interest_In_5G」、「Interest_in_Unlimited_Dataplan」或「Interest_in_iPhone_accessories」。

### 金融服務

行銷人員想要為已訂閱或取消訂閱退休金計畫或退休計畫電子報的客戶最佳化優惠。 金融服務公司可從自己的CRM將多個CustomerID擷取至Adobe Experience Platform，從自己的離線資料建立對象，並將進入和退出對象的設定檔傳送至[!DNL Pega Customer Decision Hub]，以便在傳出頻道中做出次佳動作(NBA)決策。

## 先決條件 {#prerequisites}

使用此目的地將資料匯出Adobe Experience Platform之前，請務必先在[!DNL Pega Customer Decision Hub]中完成下列必要條件：

* 在您的[!DNL Pega Customer Decision Hub]執行個體中設定[Adobe Experience Platform設定檔和對象成員資格整合元件](https://docs.pega.com/bundle/components/page/customer-decision-hub/components/adobe-membership-component.html)。
* 在您的[!DNL Pega Customer Decision Hub]執行個體中使用使用者端認證[&#128279;](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html)授與型別，設定OAuth 2.0 使用者端註冊。
* 設定[!DNL Pega Customer Decision Hub]執行個體中Adobe對象成員資格資料流程的[即時執行資料流程](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html)。

## 支援的身分 {#supported-identities}

[!DNL Pega Customer Decision Hub]支援啟用下表中描述的自訂使用者ID。 如需詳細資訊，請參閱[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 |
|---|---|
| *CustomerID* | 在[!DNL Pega Customer Decision Hub]和Adobe Experience Platform中唯一識別設定檔的一般使用者識別碼 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 匯出具有識別碼(*CustomerID*)、屬性（姓氏、名字、位置等）和對象成員資格資料之對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地永遠是以API為基礎的連線。 在Experience Platform中更新設定檔後，根據對象評估，聯結器會立即將更新傳送至下游的目的地平台。 如需詳細資訊，請參閱[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

#### OAuth 2使用者端憑證驗證 {#oauth-2-client-credentials-authentication}

![UI熒幕的影像，您可在此使用OAuth 2搭配使用者端憑證驗證，連線至Pega CDH目的地](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

填寫下列欄位並選取&#x200B;**[!UICONTROL 連線到目的地]**：

* **[!UICONTROL 存取權杖URL]**： [!DNL Pega Customer Decision Hub]執行個體上的OAuth 2存取權杖URL。
* **[!UICONTROL 使用者端識別碼]**：您在[!DNL Pega Customer Decision Hub]執行個體中產生的OAuth 2 [!DNL client ID]。
* **[!UICONTROL 使用者端密碼]**：您在[!DNL Pega Customer Decision Hub]執行個體中產生的OAuth 2 [!DNL client secret]。

### 填寫目標詳細資訊 {#destination-details}

建立與[!DNL Pega Customer Decision Hub]的驗證連線後，請提供目的地的下列資訊：

![顯示Pega CDH目的地詳細資訊已完成欄位的UI畫面影像](../../assets/catalog/personalization/pega/pega-connect-destination.png)

若要設定目的地的詳細資料，請填寫必填欄位，然後選取&#x200B;**[!UICONTROL 下一步]**。

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL Pega CDH主機名稱]**：設定檔要匯出為JSON資料的Pega客戶決策中心主機名稱。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

如需啟用此目的地對象的指示，請參閱[啟用串流設定檔匯出目的地的對象資料](../../ui/activate-streaming-profile-destinations.md)。

### 目的地屬性 {#attributes}

在[[!UICONTROL 選取屬性]](../../ui/activate-streaming-profile-destinations.md#select-attributes)步驟中，Adobe建議您從[聯合結構描述](../../../profile/home.md#profile-fragments-and-union-schemas)中選取唯一識別碼。 選取唯一識別碼以及您要匯出至目的地的任何其他XDM欄位。

### 對應範例：在[!DNL Pega Customer Decision Hub]中啟用設定檔更新 {#mapping-example}

以下是將設定檔匯出至[!DNL Pega Customer Decision Hub]時的正確身分對應範例。

選取來源欄位：

* 選取識別碼（例如：CustomerID）作為來源識別碼，以唯一識別Adobe Experience Platform和[!DNL Pega Customer Decision Hub]中的設定檔。
* 選取需要在[!DNL Pega Customer Decision Hub]中匯出和更新的XDM來源設定檔屬性變更。

選取目標欄位：

* 選取`CustomerID`名稱空間作為目標身分。
* 選取需要對應至對應XDM來源設定檔屬性的目的地設定檔屬性名稱。

![身分對應](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

成功更新設定檔的對象成員資格時，會在Pega行銷對象成員資格資料存放區中插入對象識別碼、名稱和狀態。 成員資格資料與[!DNL Pega Customer Decision Hub]中使用客戶設定檔Designer的客戶相關聯，如下所示。
![UI畫面影像，您可在此使用客戶設定檔Designer，將Adobe對象會籍資料與客戶建立關聯](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

對象會籍資料用於Pega下一個最佳動作Designer參與政策中的下一個最佳動作決策，如下所示。
![UI畫面影像，您可在其中新增對象成員資格欄位，作為Pega下一個最佳動作Designer的參與政策條件](../../assets/catalog/personalization/pega/pega-profile-designer-engagement.png)

客戶受眾會籍資料欄位會新增為最適化模型中的預測值，如下所示。
![UI熒幕的影像，您可以在其中使用Prediction Studio將Audience會籍欄位新增為最適化模型中的預測值](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## 其他資源 {#additional-resources}

如需詳細資訊，請參閱下列[!DNL Pega]檔案資源：

* [正在設定OAuth 2.0使用者端註冊](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html)
* [正在建立資料流程的即時執行](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html)
* [在客戶設定檔Designer中管理客戶記錄](https://docs.pega.com/bundle/customer-decision-hub/page/customer-decision-hub/implement/profile-designer-data-management.html)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。
