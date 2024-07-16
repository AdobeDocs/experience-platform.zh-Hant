---
keywords: 行動；炫耀；傳訊；
title: 硬式連線
description: Braze是全方位的客戶參與平台，可在客戶與所喜愛品牌之間提供相關且令人難忘的體驗。
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 2%

---

# [!DNL Braze]個連線

## 概觀 {#overview}

[!DNL Braze]目的地可協助您將設定檔資料傳送至[!DNL Braze]。

[!DNL Braze]是全方位的客戶參與平台，可在客戶與其喜愛的品牌之間提供相關且難忘的體驗。

若要將設定檔資料傳送至[!DNL Braze]，您必須先連線至目的地。

## 目的地詳情 {#specifics}

請注意[!DNL Braze]目的地專屬的下列詳細資料：

* [!DNL Adobe Experience Platform]個對象已匯出至`AdobeExperiencePlatformSegments`屬性下的[!DNL Braze]。

>[!NOTE]
>
>請記住，傳送其他自訂屬性至[!DNL Braze]可能會導致[!DNL Braze]資料點使用量增加。 請先洽詢您的[!DNL Braze]帳戶管理員，再傳送其他自訂屬性。

## 使用案例 {#use-cases}

身為行銷人員，我想要在行動參與目的地中鎖定使用者，並以[!DNL Adobe Experience Platform]內建對象。 此外，我想要在[!DNL Adobe Experience Platform]中更新對象和設定檔時，根據其[!DNL Adobe Experience Platform]設定檔中的屬性，為他們提供個人化體驗。

## 支援的身分 {#supported-identities}

[!DNL Braze]支援下表所述的身分啟用。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| external_id | 支援任何身分對應的自訂[!DNL Braze]識別碼。 | 只要您將任何[身分識別](../../../identity-service/features/namespaces.md)對應到[!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation)，就可以將其傳送到[!DNL Braze]目的地。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform[細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ (A) | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構欄位（例如：電子郵件地址、電話號碼、姓氏）和/或身分，視您的欄位對應而定。[!DNL Adobe Experience Platform]個對象已匯出至`AdobeExperiencePlatformSegments`屬性下的[!DNL Braze]。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

* **[!UICONTROL 硬碟帳戶Token]**：這是您的[!DNL Braze] [!DNL API]金鑰。 您可以在這裡找到有關如何取得[!DNL API]金鑰的詳細說明： [REST API金鑰概述](https://www.braze.com/docs/api/api_key/)。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：輸入您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：輸入有助於您日後識別此目的地的描述。
* **[!UICONTROL 端點執行個體]**：請詢問您的[!DNL Braze]代表您應該使用哪個端點執行個體。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

如需啟用此目的地的對象的指示，請參閱[啟用串流對象匯出目的地的對象資料](../../ui/activate-segment-streaming-destinations.md)。

## 對應考量事項 {#mapping-considerations}

若要將對象資料從[!DNL Adobe Experience Platform]正確傳送至[!DNL Braze]目的地，您必須完成欄位對應步驟。

對應包括在[!DNL Platform]帳戶中的[!DNL Experience Data Model] (XDM)結構描述欄位之間建立連結，以及從目標目的地建立對應對應專案。

若要將您的XDM欄位正確對應到[!DNL Braze]目的地欄位，請遵循下列步驟：

在[!UICONTROL 對應]步驟中，按一下&#x200B;**[!UICONTROL 新增對應]**。

![硬碟目的地新增對應](../../assets/catalog/mobile-engagement/braze/mapping.png)

在[!UICONTROL Source欄位]區段中，按一下空白欄位旁的箭頭按鈕。

![硬碟目的地Source對應](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

在[!UICONTROL 選取來源欄位]視窗中，您可以在兩種類別的XDM欄位之間進行選擇：
* [!UICONTROL 選取屬性]：使用此選項將您XDM結構描述中的特定欄位對應到[!DNL Braze]屬性。

![硬碟目的地對應Source屬性](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL 選取身分名稱空間]：使用此選項將[!DNL Platform]身分名稱空間對應至[!DNL Braze]名稱空間。

![硬碟目的地對應Source名稱空間](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

選擇您的來源欄位，然後按一下&#x200B;**[!UICONTROL 選取]**。

在[!UICONTROL 目標欄位]區段中，按一下欄位右側的對應圖示。

![硬碟目的地目標對應](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

在[!UICONTROL 選取目標欄位]視窗中，您可以選擇兩種目標欄位類別：
* [!UICONTROL 選取身分名稱空間]：使用此選項將[!DNL Platform]身分名稱空間對應到[!DNL Braze]身分名稱空間。
* [!UICONTROL 選取自訂屬性]：使用此選項將XDM屬性對應到您在[!DNL Braze]帳戶中定義的自訂[!DNL Braze]屬性。 <br>您也可以使用此選項將現有的XDM屬性重新命名為[!DNL Braze]。 例如，將`lastName` XDM屬性對應至[!DNL Braze]中的自訂`Last_Name`屬性，將在[!DNL Braze]中建立`Last_Name`屬性（如果尚未存在），並將`lastName` XDM屬性對應至該屬性。

![硬碟目的地目標對應欄位](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

選擇您的目標欄位，然後按一下&#x200B;**[!UICONTROL 選取]**。

您現在應該會在清單中看到您的欄位對應。

![硬碟目的地對應完成](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

若要新增更多對應，請重複上述步驟。

## 對應範例 {#mapping-example}

假設您的XDM設定檔結構描述和[!DNL Braze]執行個體包含以下屬性和身分：

|  | XDM設定檔結構描述 | [!DNL Braze]執行個體 |
|---|---|---|
| 屬性 | <ul><li><code>person.name.firstname</code></li><li><code>person.name.lastName</code></li><li><code>行動電話。號碼</code></li></ul> | <ul><li><code>名字</code></li><li><code>姓氏</code></li><li><code>電話號碼</code></li></ul> |
| 身分 | <ul><li><code>電子郵件</code></li><li><code>Google廣告ID (GAID)</code></li><li>廣告商的<code>Apple ID (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

正確的對應如下所示：

![硬碟目的地對應範例](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## 匯出的資料 {#exported-data}

若要確認資料是否已成功匯出至[!DNL Braze]目的地，請檢查您的[!DNL Braze]帳戶。 [!DNL Adobe Experience Platform]個對象已匯出至`AdobeExperiencePlatformSegments`屬性下的[!DNL Braze]。

## 疑難排解 {#troubleshooting}

**我在啟用我的對象到此目的地時收到逾時錯誤。 我應該怎麼做？**

有時，此目的地的對象啟用可能會導致逾時錯誤。 此錯誤並不表示有啟用問題。

如果您收到逾時錯誤，請檢查目的地平台中的對象人數。 如果對象人數正確，則整合可如預期運作。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](../../../data-governance/home.md)。
