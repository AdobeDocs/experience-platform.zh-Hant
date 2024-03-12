---
title: 設定資料串流的機器人偵測
description: 瞭解如何為資料串流設定機器人偵測，以區分人類和非人類流量。
hide: true
hidefromtoc: true
exl-id: 6b221d97-0145-4d3e-a32d-746d72534add
source-git-commit: 7757cd869607bf25bff1e9861732cf4b80b38966
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 0%

---

# 設定資料串流的機器人偵測

源自非人類實體（例如自動化程式、網頁刮刀、編目程式、指令碼掃描器）的流量，會使得識別來自人類訪客的事件變得更加困難。 此類流量可能會對重要的商業量度產生負面影響，導致不正確的流量報表。

機器人偵測可讓您識別系統產生的事件，[Web SDK](../web-sdk/home.md)， [行動SDK](https://developer.adobe.com/client-sdks/home/) 和 [[!DNL Server API]](../server-api/overview.md) 由已知的編目程式和機器人所產生。

透過為資料串流設定機器人偵測，您可以識別要分類為機器人事件的特定IP位址、IP範圍和請求標題。

識別機器人流量可讓您更準確地測量使用者在您網站或行動應用程式上的活動。

當對Edge Network的請求符合任何機器人偵測規則時，XDM結構描述會以機器人評分（一律設為1）更新，如下所示。

```json
{
  "botDetection": {
    "score": 1
  }
}
```

此機器人分數可協助接收請求的解決方案正確識別機器人流量。

>[!IMPORTANT]
>
>機器人偵測不會捨棄任何機器人請求。 它只會以機器人分數更新XDM結構描述，並將事件轉送至 [資料流服務](configure.md) 您已設定的。
>
>Adobe解決方案可能會以不同的方式處理機器人評分。 例如，Adobe Analytics使用其 [機器人篩選服務](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/bot-removal/bot-rules.html) 而且不會使用Edge Network設定的分數。 這兩個服務使用相同的 [IAB機器人清單](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/)，因此機器人分數相同。

建立機器人偵測規則後，可能需要最多15分鐘的時間才能傳播至Edge Network。

## 先決條件 {#prerequisites}

為了讓機器人偵測對您的資料流有效，您必須新增 **[!UICONTROL 機器人偵測資訊]** 欄位群組至您的結構描述。 請參閱 [XDM結構描述](../xdm/ui/resources/schemas.md#add-field-groups) 有關如何將欄位群組新增到結構描述的檔案。

## 設定資料串流的機器人偵測 {#configure}

您可以在建立資料流設定後設定機器人偵測。 請參閱檔案，瞭解如何 [建立和設定資料串流](configure.md)，然後依照下列指示，將機器人偵測功能新增至資料流。

移至資料串流清單，並選取您要新增機器人偵測的資料串流。

![顯示資料流清單的資料流使用者介面。](assets/bot-detection/datastream-list.png)

在資料流詳細資訊頁面中，選取 **[!UICONTROL 機器人偵測]** 選項。

![在資料串流使用者介面中反白顯示的機器人偵測選項。](assets/bot-detection/bot-detection.png)

此 **[!UICONTROL 機器人偵測規則]** 頁面隨即顯示。

![資料流設定頁面中的機器人偵測設定。](assets/bot-detection/bot-detection-page.png)

在「機器人偵測規則」頁面中，您可以使用下列功能來設定機器人偵測：

* 使用 [!DNL [IAB/ABC International Spiders and Bots List]](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/).
* 建立您自己的機器人偵測規則。

### 使用IAB/ABC國際編目程式與機器人清單 {#iab-list}

此 [IAB/ABC國際編目程式與機器人清單](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/) 是協力廠商的業界標準網際網路編目程式和機器人清單，可協助您識別自動流量，例如搜尋引擎編目程式、監控工具，以及其他您可能不想顯示在分析計數中的非人類流量。

若要設定您的資料串流以使用 [!DNL IAB/ABC International Spiders and Bots List]，切換 **[!UICONTROL 在此資料流中使用IAB/ABC國際編目程式和機器人清單進行機器人偵測]** 選項，然後選取「儲存」以將機器人偵測設定套用至資料流。

![IAB編目程式和機器人清單已啟用。](assets/bot-detection/bot-detection-list.png)

### 建立機器人偵測規則 {#rules}

除了使用 [IAB/ABC國際編目程式與機器人清單](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/)，您可以為每個資料流定義自己的機器人偵測規則。

您可以根據以下專案建立機器人偵測規則： **IP位址** 和 **IP位址範圍**.

如果您需要更精細的機器人偵測規則，可將IP條件與請求標頭條件結合。 機器人偵測規則可以使用以下標頭：

| HTTP 標題 | 說明 |
| --- | --- |
| `user-agent` | 標頭，可讓伺服器和網路對等識別請求使用者代理程式的應用程式、作業系統、廠商和/或版本。 |
| `content-type` | 表示資源的原始媒體型別（在套用用於傳送的任何內容編碼之前）。 |
| `referer` | 識別要求資源的網頁位址。 |
| `sec-ch-ua` | 以逗號分隔清單形式提供與瀏覽器相關聯的每個品牌的品牌和重要版本。 |
| `sec-ch-ua-mobile` | 指出瀏覽器是否位在行動裝置上。 案頭瀏覽器也可以使用它來表示行動使用者體驗的偏好設定。 |
| `sec-ch-ua-platform` | 提供執行使用者代理程式的平台或作業系統。 例如：「Windows」或「Android」。 |
| `sec-ch-ua-platform-version` | 提供執行使用者代理程式的作業系統版本。 |
| `sec-ch-ua-arch` | 提供使用者代理程式的基礎CPU架構，例如ARM或x86。 |
| `sec-ch-ua-model` | 表示執行瀏覽器的裝置型號。 |
| `sec-ch-ua-bitness` | 提供使用者代理程式基礎CPU架構的「位元」。 這是整數或記憶體位址的位元大小，通常是64或32位元。 |
| `sec-ch-ua-wow64` | 指出使用者代理程式二進位檔是否在64位元Windows上以32位元模式執行。 |

若要建立機器人偵測規則，請遵循下列步驟：

1. 選取 **[!UICONTROL 新增規則]**.

   ![機器人偵測設定畫面會醒目顯示「新增規則」按鈕。](assets/bot-detection/bot-detection-new-rule.png)

2. 在「 」中輸入規則的名稱 **[!UICONTROL 規則名稱]** 欄位。

   ![反白顯示規則名稱的機器人偵測規則畫面。](assets/bot-detection/rule-name.png)

3. 選取 **[!UICONTROL 新增IP條件]** 以新增以IP為基礎的規則。 您可以依IP位址或IP位址範圍定義規則。

   ![機器人偵測規則畫面，其中的IP位址欄位會反白顯示。](assets/bot-detection/ip-address-rule.png)

   ![機器人偵測規則畫面，其中的IP範圍欄位會反白顯示。](assets/bot-detection/ip-range-rule.png)

   >[!TIP]
   >
   >IP條件是以邏輯 `OR` 作業。 如果符合您定義的任何IP條件，則會將請求標示為源自機器人。

4. 如果您想要將標題條件新增至規則，請選取 **[!UICONTROL 新增標頭條件群組]**，然後選取您要規則使用的標頭。

   ![反白標頭條件的機器人偵測規則畫面。](assets/bot-detection/header-conditions.png)

   然後，新增用於所選標頭的條件。

   ![反白標頭條件的機器人偵測規則畫面。](assets/bot-detection/header-condition-rule.png)

5. 設定所需的機器人偵測規則後，選取 **[!UICONTROL 儲存]** 將規則套用至資料流。

   ![反白標頭條件的機器人偵測規則畫面。](assets/bot-detection/bot-detection-save.png)


## 機器人偵測規則範例 {#examples}

若要協助您開始使用機器人偵測功能，您可以使用下列範例建立機器人偵測規則。

### 根據一個IP位址偵測機器人 {#one-ip}

若要將所有來自特定IP位址的請求標示為機器人流量，請建立新的機器人偵測規則，以評估單一IP位址，如下圖所示。

![根據一個IP位址的機器人偵測規則。](assets/bot-detection/bot-detection-one-ip.png)

### 根據兩個IP位址進行機器人偵測 {#two-ip}

若要將所有來自兩個特定IP位址其中一個的請求標示為機器人流量，請建立新的機器人偵測規則，以評估兩個IP位址，如下圖所示。

![根據兩個IP位址的機器人偵測規則。](assets/bot-detection/bot-detection-two-ips.png)

### 根據IP位址範圍的機器人偵測 {#range}

若要將源自特定範圍內任何IP位址的所有要求標示為機器人流量，請建立新的機器人偵測規則，以評估整個IP位址範圍，如下圖所示。

![機器人偵測規則以IP範圍為基礎。](assets/bot-detection/bot-detection-range.png)

### 根據IP位址和請求標題進行機器人偵測 {#ip-header}

若要將源自特定IP位址且包含特定請求標題的所有請求標示為機器人流量，請建立新的機器人偵測規則，如下圖所示。

此規則會檢查要求是否源自特定IP位址，以及 `referer` 請求標頭開頭為 `www.adobe.com`.

![根據IP位址和請求標題的機器人偵測規則。](assets/bot-detection/bot-detection-header-ip.png)

### 根據多個條件的機器人偵測 {#multiple-conditions}

您可以根據以下專案建立機器人偵測規則：

* **多個不同條件**：不同的條件會評估為邏輯 `AND` 作業，這表示需要同時符合條件，才能將請求識別為源自機器人。
* **相同型別的多個條件**：將相同型別的條件評估為邏輯 `OR` 作業，這表示如果符合任何條件，則會將請求識別為源自機器人。

如果符合下列條件，下圖顯示的規則會識別機器人起始的請求：

該請求源自兩個IP位址中的一個， `referer` 標題開頭為 `www.adobe.com`，以及 `sec-ch-ua-mobile` 標題會將請求識別為源自於案頭瀏覽器。

![機器人偵測規則是根據多個條件。](assets/bot-detection/bot-detection-multiple.png)
