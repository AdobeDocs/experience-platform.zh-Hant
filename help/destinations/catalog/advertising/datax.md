---
title: Verizon MediaYahoo DataX連線
description: DataX是彙總的Verizon Media/Yahoo基礎架構，其中託管各種元件，讓Verizon Media/Yahoo能夠以安全、自動化及可擴充的方式與外部合作夥伴交換資料。
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 3%

---

# [!DNL Verizon Media/Yahoo DataX]個連線

## 概觀 {#overview}

[!DNL DataX]是彙總的[!DNL Verizon Media/Yahoo]基礎結構，其中裝載各種元件，讓[!DNL Verizon Media/Yahoo]能夠與其外部合作夥伴以安全、自動化及可擴充的方式交換資料。

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由[!DNL Verizon Media/Yahoo]的[!DNL DataX]團隊建立和維護。 若有任何查詢或更新要求，請直接透過[dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)聯絡他們

## 先決條件 {#prerequisites}

**MDM ID**

這是[!DNL Yahoo DataX]中的唯一識別碼，也是設定資料匯出至此目的地的必要欄位。 如果您不知道此ID，請連絡您的[!DNL Yahoo DataX]帳戶管理員。

**分類中繼資料**

分類資源定義基底[!DNL DataX]中繼資料結構的延伸

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

在[!DNL DataX]開發人員檔案中進一步瞭解[分類中繼資料](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/)。

## 比率限制和護欄 {#rate-limits-guardrails}

>[!IMPORTANT]
>
>將超過100個對象啟用至[!DNL Verizon Media/Yahoo DataX]時，您可能會收到來自目的地的速率限制錯誤。 將對象啟用至此目的地時，請嘗試在一個啟用資料流中啟用少於100個對象。 如果您需要啟用更多區段，請在相同帳戶上建立新目的地。

根據[DataX檔案](https://developer.verizonmedia.com/datax/guide/rate-limits/)中概述的分類法和對象貼文配額限制，[!DNL DataX]是速率限制。


| 錯誤碼 | 錯誤訊息 | 說明 |
|---------|----------|---------|
| 429太多請求 | 超過每小時的速率限制&#x200B;**（限制： 100）** | 每個提供者一小時內允許的請求數。 |

{style="table-layout:auto"}

## 支援的身分 {#supported-identities}

[!DNL Verizon Media]支援下表所述的身分啟用。 深入瞭解[身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 |
| GAID | GOOGLE ADVERTISING ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取IDFA目標身分。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出具有Verizon Media目的地中所使用識別碼（電子郵件、GAID、IDFA）之對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 使用案例 {#use-cases}

[!DNL DataX] API可供廣告商使用，這些廣告商想要鎖定在[!DNL Verizon Media] (VMG)中電子郵件地址以外的特定對象群組，可以使用VMG的近乎即時API快速建立新對象並推送所需的對象群組。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

![Experience Platform UI中的Yahoo DataX目的地卡](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL MDM識別碼]**：這是[!DNL Yahoo DataX]中的唯一識別碼，是設定資料匯出至此目的地的必要欄位。 如果您不知道此ID，請連絡您的[!DNL Yahoo DataX]帳戶管理員。  使用MDM ID時，資料可以限製為僅用於特定一組專屬使用者（例如廣告商的第一方資料）。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至目的地](../../ui/activate-segment-streaming-destinations.md)，以取得啟用對象至目的地的指示。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)。

## 其他資源 {#additional-resources}

如需詳細資訊，請參閱 [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/)上的[!DNL Yahoo/Verizon Media] [檔案。
