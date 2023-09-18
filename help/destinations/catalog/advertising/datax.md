---
title: Verizon MediaYahoo DataX連線
description: DataX是彙總的Verizon Media/Yahoo基礎架構，其中託管各種元件，讓Verizon Media/Yahoo能夠以安全、自動化及可擴充的方式與外部合作夥伴交換資料。
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '817'
ht-degree: 2%

---

# [!DNL Verizon Media/Yahoo DataX] 連線

## 概觀 {#overview}

[!DNL DataX] 是彙總 [!DNL Verizon Media/Yahoo] 代管各種元件的基礎結構，這些元件可 [!DNL Verizon Media/Yahoo] 以安全、自動化及可擴充的方式與外部合作夥伴交換資料。

>[!IMPORTANT]
>
>建立和維護此目的地聯結器和檔案頁面的人員為 [!DNL Verizon Media/Yahoo]的 [!DNL DataX] 團隊。 如有任何查詢或更新要求，請直接聯絡他們： [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## 先決條件 {#prerequisites}

**MDM ID**

此為中的唯一識別碼 [!DNL Yahoo DataX] 而且這是設定資料匯出至此目的地的必要欄位。 如果您不知道此ID，請連絡您的 [!DNL Yahoo DataX] 客戶經理。

**分類中繼資料**

分類資源會定義基底上的擴充功能 [!DNL DataX] 中繼資料結構

```
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

深入瞭解 [分類中繼資料](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) 在 [!DNL DataX] 開發人員檔案。

## 比率限制和護欄 {#rate-limits-guardrails}

>[!IMPORTANT]
>
>將超過100個對象啟用至 [!DNL Verizon Media/Yahoo DataX]，您可能會收到來自目的地的速率限制錯誤。 將對象啟用至此目的地時，請嘗試在一個啟用資料流中啟用少於100個對象。 如果您需要啟用更多區段，請在相同帳戶上建立新目的地。

[!DNL DataX] 是費率限制，依據以下章節中概述的分類法和受眾貼文配額限制： [DataX檔案](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| 錯誤碼 | 錯誤訊息 | 說明 |
|---------|----------|---------|
| 429太多請求 | 每小時超過速率限制 **（上限： 100）** | 每個提供者一小時內允許的請求數。 |

{style="table-layout:auto"}

## 支援的身分 {#supported-identities}

[!DNL Verizon Media] 支援下表所述的身分啟用。 進一步瞭解 [身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| GAID | Google廣告ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取IDFA目標身分。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在匯出具有Verizon Media目的地中所使用識別碼（電子郵件、GAID、IDFA）之對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 使用案例 {#use-cases}

[!DNL DataX] API適用於廣告商，他們想要鎖定中的特定受眾群組，以中斷電子郵件地址的連結。 [!DNL Verizon Media] (VMG)可以使用VMG的近乎即時API快速建立新受眾並推送所需的受眾群組。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

![Platform UI中的Yahoo DataX目的地卡](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 連線引數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊給此目的地：

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL MDM ID]**：這是中的唯一識別碼 [!DNL Yahoo DataX] 而且這是設定資料匯出至此目的地的必要欄位。 如果您不知道此ID，請連絡您的 [!DNL Yahoo DataX] 客戶經理。  使用MDM ID時，資料可以限製為僅用於特定一組專屬使用者（例如廣告商的第一方資料）。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟用此目的地的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

讀取 [對目的地啟用設定檔和對象](../../ui/activate-segment-streaming-destinations.md) 以取得啟用目的地對象的指示。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，請參閱 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant).

## 其他資源 {#additional-resources}

如需詳細資訊，請閱讀 [!DNL Yahoo/Verizon Media] [檔案： [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
