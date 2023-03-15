---
title: Pega客戶決策中心連線
description: 使用Adobe Experience Platform中的Pega客戶決策中心目的地，將設定檔屬性和區段成員資料傳送至Pega客戶決策中心，以便做出下一個最佳動作決策。
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: ae00b113308354e98f4448d2544e2a6e475c384e
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Pega客戶決策中心連線

## 總覽 {#overview}

使用 [!DNL Pega Customer Decision Hub] 目的地，將設定檔屬性和區段成員資格資料傳送至 [!DNL Pega Customer Decision Hub] 以決定下一個最佳動作。

從Adobe Experience Platform載入至時的設定檔區段成員資格 [!DNL Pega Customer Decision Hub]，可作為最適化模型中的預測值，並協助您提供正確的情境和行為資料，以便做出下一個最佳動作決策。

>[!IMPORTANT]
>
>此文檔頁由Pegasystems建立。 如有任何查詢或更新請求，請直接與Pega聯繫 [此處](mailto:support@pega.com).

## 使用案例

以協助您更清楚了解應如何及何時使用 [!DNL Customer Decision Hub] 目的地，以下是Adobe Experience Platform客戶可透過此目的地解決的範例使用案例。

### 電信

行銷人員想要運用資料科學模型所提供之下一個最佳動作的深入分析，由 [!DNL Pega Customer Decision Hub] 客戶參與。 [!DNL Pega Customer Decision Hub] 嚴重依賴客戶意圖 — 例如「Interest_In_5G」、「Intested_in_Unlimited_Dataplan」或「Interest_in_iPhone_accessories」。

### 金融服務

行銷人員想要針對已訂閱或取消訂閱退休金計畫或退休計畫電子報的客戶，最佳化優惠方案。 金融服務公司可以將多個客戶ID從自己的CRM擷取至Adobe Experience Platform、從自己的離線資料建立區段，以及將輸入和退出區段的設定檔傳送至 [!DNL Pega Customer Decision Hub] 對外頻道的下一最佳動作(NBA)決策。

## 先決條件 {#prerequisites}

使用此目的地將資料匯出Adobe Experience Platform之前，請務必完成下列必要條件： [!DNL Pega Customer Decision Hub]:

* 設定 [Adobe Experience Platform設定檔和區段成員資格整合元件](https://docs.pega.com/component/customer-decision-hub/adobe-experience-platform-profile-and-segment-membership-integration-component) 在 [!DNL Pega Customer Decision Hub] 例項。
* 設定OAuth 2.0 [使用客戶端憑據註冊客戶端](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) 您的 [!DNL Pega Customer Decision Hub] 例項。
* 設定 [即時執行資料流](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) Adobe區段成員資格資料流程 [!DNL Pega Customer Decision Hub] 例項。

## 支援的身分 {#supported-identities}

[!DNL Pega Customer Decision Hub] 支援啟動下表所述的自訂使用者ID。 如需詳細資訊，請參閱 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 |
|---|---|
| *CustomerID* | 唯一識別設定檔的通用使用者識別碼，位於 [!DNL Pega Customer Decision Hub] 和Adobe Experience Platform |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 匯出具有識別碼(*CustomerID*)、屬性（姓氏、名字、位置等） 和區段成員資格資料。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地一律以API為基礎的連線。 在Experience Platform中更新設定檔時，連接器會根據區段評估，將更新下游傳送至目的地平台。 如需詳細資訊，請參閱 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 連接到目標 {#connect}

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫下列兩節所列的欄位。

### 驗證到目標 {#authenticate}

#### OAuth 2用戶端認證驗證 {#oauth-2-client-credentials-authentication}

![使用OAuth 2搭配用戶端憑證驗證以連線至Pega CDH目的地的UI畫面影像](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

填寫下面的欄位並選取 **[!UICONTROL 連接到目標]**:

* **[!UICONTROL 存取權杖URL]**:您的 [!DNL Pega Customer Decision Hub] 例項。
* **[!UICONTROL 用戶端ID]**:OAuth 2 [!DNL client ID] 由 [!DNL Pega Customer Decision Hub] 例項。
* **[!UICONTROL 用戶端密碼]**:OAuth 2 [!DNL client secret] 由 [!DNL Pega Customer Decision Hub] 例項。

### 填寫目的地詳細資訊 {#destination-details}

建立與 [!DNL Pega Customer Decision Hub]，請提供目的地的下列資訊：

![UI畫面的影像，顯示Pega CDH目的地詳細資訊的已完成欄位](../../assets/catalog/personalization/pega/pega-connect-destination.png)

若要設定目的地的詳細資訊，請填寫必填欄位並選取 **[!UICONTROL 下一個]**.

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 主機名稱]**:設定檔會匯出為JSON資料的Pega客戶決策中心主機名稱。

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [對串流設定檔匯出目的地啟用受眾資料](../../ui/activate-streaming-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

### 目標屬性 {#attributes}

在 [[!UICONTROL 選擇屬性]](../../ui/activate-streaming-profile-destinations.md#select-attributes) 步驟，Adobe建議您從 [聯合方案](../../../profile/home.md#profile-fragments-and-union-schemas). 選取唯一識別碼，以及您要匯出至目的地的任何其他XDM欄位。

### 對應範例：啟用設定檔更新 [!DNL Pega Customer Decision Hub] {#mapping-example}

以下是將設定檔匯出至時的正確身分對應範例 [!DNL Pega Customer Decision Hub].

選擇源欄位：

* 選取識別碼(例如：CustomerID)作為來源識別，可唯一識別Adobe Experience Platform和 [!DNL Pega Customer Decision Hub].
* 選取需要匯出和更新的XDM來源設定檔屬性變更。 [!DNL Pega Customer Decision Hub].

選擇目標欄位：

* 選取 `CustomerID` 命名空間作為目標身份。
* 選取需要對應至對應XDM來源設定檔屬性的目標設定檔屬性名稱。

![身分對應](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## 匯出的資料/驗證資料匯出 {#exported-data}

成功更新設定檔的區段成員資格後，會在Pega行銷區段成員資格資料存放區中插入區段識別碼、名稱和狀態。 會籍資料與使用客戶設定檔設計工具的客戶相關聯，位於 [!DNL Pega Customer Decision Hub]，如下所示。
![UI畫面的影像，您可以使用客戶設定檔設計工具，將Adobe區段成員資格資料與客戶建立關聯](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

區段成員資格資料用於Pega下一最佳動作設計器參與政策，以便做出下一個最佳動作決策，如下所示。
![UI畫面的影像，您可以在Pega Next-Best-Action Designer的參與原則中新增「區段成員資格」欄位作為條件](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

客戶區段成員資格資料欄位會在適用性模型中新增為預測器，如下所示。
![UI畫面的影像，您可使用Prediction Studio在適用性模型中新增「區段」成員欄位作為預測器](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## 其他資源 {#additional-resources}

請參閱 [設定OAuth 2.0用戶端註冊](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) in [!DNL Pega Customer Decision Hub].

請參閱 [為資料流建立即時執行](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) in [!DNL Pega Customer Decision Hub].

請參閱 [在客戶設定檔設計工具中管理客戶記錄](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](/help/data-governance/home.md).
