---
title: Verizon MediaYahoo DataX連線
description: DataX是Verizon Media/Yahoo的聚合基礎架構，它承載各種元件，使Verizon Media/Yahoo能夠以安全、自動化和可擴展的方式與其外部合作夥伴交換資料。
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 2%

---

# Verizon Media/Yahoo DataX連線

## 總覽 {#overview}

DataX是Verizon Media/Yahoo的聚合基礎架構，它承載各種元件，使Verizon Media/Yahoo能夠以安全、自動化和可擴展的方式與其外部合作夥伴交換資料。

>[!IMPORTANT]
>
>此檔案頁面是由Verizon Media/Yahoo的DataX團隊建立。 如有任何查詢或更新請求，請直接與他們聯繫，地址為 [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## 先決條件 {#prerequisites}

**MDM ID**

這是Yahoo DataX中的唯一識別碼，也是設定匯出至此目的地的資料的必要欄位。 如果您不知道此ID，請連絡您的Yahoo Data X客戶經理。

**速率限制**

DataX會根據 [DataX檔案](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| 錯誤代碼 | 錯誤訊息 | 說明 |
|---------|----------|---------|
| 429請求太多 | 超出的速率限制 **(限制：100)** | 每個提供程式一小時內允許的請求數。 |

{style=&quot;table-layout:auto&quot;}

**分類元資料**

分類資源定義基本DataX元資料結構上的擴展

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

深入了解 [分類元資料](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) 在DataX開發人員檔案中。

## 支援的身分 {#supported-identities}

Verizon Media支援啟用下表所述的身分識別。 深入了解 [身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請檢查 **[!UICONTROL 套用轉換]** 選項，必須 [!DNL Platform] 啟動時自動雜湊資料。 |
| GAID | Google Advertising ID | 當源標識為GAID命名空間時，選擇GAID目標標識。 |
| IDFA | Apple ID for Advertisers | 如果來源識別為IDFA命名空間，請選取IDFA目標識別。 |

{style=&quot;table-layout:auto&quot;}

## 匯出類型 {#export-type}

**區段匯出**  — 您正在匯出區段（對象）的所有成員，以及Verizon媒體目的地所使用的識別碼（電子郵件）。

## 使用案例 {#use-cases}

廣告商若想鎖定在Verizon Media(VMG)中輸入電子郵件地址的特定對象群組，可使用VMG的近乎即時API快速建立新區段，並推送所需的對象群組，即可使用DataX API。

## 連接到目標 {#connect}

![Platform UI中的Yahoo DataX目的地卡](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL MDM ID]**:這是Yahoo DataX中的唯一識別碼，也是設定匯出至此目的地的資料的必要欄位。 如果您不知道此ID，請連絡您的Yahoo Data X客戶經理。  使用MDM ID時，資料只能被限制用於特定的專用用戶集（例如廣告商的第一方資料）。

## 啟用此目的地的區段 {#activate}

閱讀 [將設定檔和區段啟用至目的地](../../ui/activate-segment-streaming-destinations.md) 關於在目的地啟用受眾區段的指示。

## 資料使用與控管 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 處理資料時，目的地符合資料使用原則。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料控管，請參閱 [資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## 其他資源 {#additional-resources}

如需詳細資訊，請參閱Yahoo/Verizon Media [DataX相關檔案](https://developer.verizonmedia.com/datax/guide/).
