---
title: Verizon MediaYahoo DataX連線
description: DataX是Verizon Media/Yahoo的聚合基礎架構，它承載各種元件，使Verizon Media/Yahoo能夠以安全、自動化和可擴展的方式與其外部合作夥伴交換資料。
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 0580816c471400ba17eddcb6b1a9dfbf01797938
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 2%

---

# [!DNL Verizon Media/Yahoo DataX] 連接

## 總覽 {#overview}

[!DNL DataX] 是匯總 [!DNL Verizon Media/Yahoo] 承載各種元件的基礎結構 [!DNL Verizon Media/Yahoo] 以安全、自動化和可擴充的方式與外部合作夥伴交換資料。

>[!IMPORTANT]
>
>此文檔頁面由 [!DNL Verizon Media/Yahoo]&#39;s [!DNL DataX] 團隊。 如有任何查詢或更新請求，請直接與他們聯繫，地址為 [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## 先決條件 {#prerequisites}

**MDM ID**

這是 [!DNL Yahoo DataX] 而且，這是設定匯出至此目的地的資料的必要欄位。 如果您不知道此ID，請連絡您的 [!DNL Yahoo DataX] 客戶經理。

**分類元資料**

分類資源定義基本的擴展 [!DNL DataX] 中繼資料結構

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

深入了解 [分類元資料](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) 在 [!DNL DataX] 開發人員檔案。

## 速率限制和護欄 {#rate-limits-guardrails}

>[!IMPORTANT]
>
>將超過100個區段啟用至 [!DNL Verizon Media/Yahoo DataX]，您可能會從目的地收到限速錯誤。 將段激活到此目標時，請嘗試在一個激活資料流中激活少於100個段。 如果您需要啟用更多區段，請在相同帳戶上建立新目的地。

[!DNL DataX] 是根據 [DataX檔案](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| 錯誤代碼 | 錯誤訊息 | 說明 |
|---------|----------|---------|
| 429請求太多 | 超出的速率限制 **(限制：100)** | 每個提供程式一小時內允許的請求數。 |

{style="table-layout:auto"}

## 支援的身分 {#supported-identities}

[!DNL Verizon Media] 支援啟用下表所述的身分。 深入了解 [身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。 |
| GAID | Google Advertising ID | 當源標識為GAID命名空間時，選擇GAID目標標識。 |
| IDFA | Apple ID for Advertisers | 如果來源識別為IDFA命名空間，請選取IDFA目標識別。 |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在匯出區段（對象）的所有成員，以及Verizon媒體目的地所使用的識別碼（電子郵件、GAID、IDFA）。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 使用案例 {#use-cases}

[!DNL DataX] 廣告商若想鎖定將電子郵件地址作為輸入資料的特定對象群組，可使用API [!DNL Verizon Media] (VMG)可以使用VMG的近乎即時API，快速建立新區段並推送所需的對象群組。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

![Platform UI中的Yahoo DataX目的地卡](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL MDM ID]**:這是 [!DNL Yahoo DataX] 而且，這是設定匯出至此目的地的資料的必要欄位。 如果您不知道此ID，請連絡您的 [!DNL Yahoo DataX] 客戶經理。  使用MDM ID時，資料只能被限制用於特定的專用用戶集（例如廣告商的第一方資料）。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

閱讀 [將設定檔和區段啟用至目的地](../../ui/activate-segment-streaming-destinations.md) 關於在目的地啟用受眾區段的指示。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant).

## 其他資源 {#additional-resources}

如需詳細資訊，請閱讀 [!DNL Yahoo/Verizon Media] [檔案 [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
