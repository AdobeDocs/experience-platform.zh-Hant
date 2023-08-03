---
title: 使用來自 DNL The Weather Channel 的天氣資料
description: 使用來自 DNL The Weather Channel 的天氣資料以增強您透過資料流收集的資料。
exl-id: 548dfca7-2548-46ac-9c7e-8190d64dd0a4
source-git-commit: 4c9abcefb279c6e8a90744b692d86746a4896d0a
workflow-type: ht
source-wordcount: '672'
ht-degree: 100%

---

# 使用來自 [!DNL The Weather Channel] 的天氣資料

Adobe 已和 [!DNL [The Weather Company]](https://www.ibm.com/weather) 合作，將美國天氣的附加內容引進透過資料流收集的資料中。您可以在 Experience Platform 中使用此資料進行分析、目標定位和區段建立。

[!DNL The Weather Channel] 可提供 3 種類型的資料：

* **[!UICONTROL 目前的天氣]**：根據使用者的位置提供目前的天氣狀況。其中包括目前的溫度、降水量、雲量等。
* **[!UICONTROL 預報的天氣]**：預報內容包括使用者所在位置的 1、2、3、5、7、10 天預報。
* **[!UICONTROL 觸發因素]**：觸發因素指對應至不同語義天氣狀況的特定組合。有三種不同類型的天氣觸發因素：

   * **[!UICONTROL 天氣觸發因素]**：具有語義意義的狀況，例如寒冷或下雨的天氣。這些在不同氣候下的定義可能有所不同。
   * **[!UICONTROL 產品觸發因素]**：會導致購買不同類型產品的狀況。例如：寒冷天氣的預報可能表示購買雨衣的可能性提高了。
   * **[!UICONTROL 惡劣天氣觸發因素]**：惡劣天氣的警告，例如冬季暴風雨或颶風警告。

## 先決條件 {#prerequisites}

在使用天氣資料之前，請確保滿足以下先決條件：

* 您必須向 [!DNL The Weather Channel] 取得將使用之天氣資料的授權。然後他們會在您的帳戶上啟用授權。
* 天氣資料只能透過資料流取得。若要使用天氣資料，您必須使用 [!DNL Web SDK]、[!DNL Mobile Edge Extension] 或是[伺服器 API](../../server-api/overview.md)，才能利用這些資料。
* 您的資料流必須啟用[[!UICONTROL 地理位置]](../configure.md#advanced-options)。
* 新增[天氣欄位群組](#schema-configuration)到您正在使用的綱要。

## 佈建 {#provisioning}

向 [!DNL The Weather Channel] 取得資料授權後，您的帳戶即會獲得啟用，可存取資料。接下來，您則必須和 Adob&#x200B;&#x200B;e 客戶服務聯絡，要求在您的資料流上啟用資料。啟用後，即會自動附加資料。

使用偵錯工具執行邊緣追蹤或使用 Assurance 追蹤通過 [!DNL Edge Network] 的點擊，即可驗證是否已新增。

### 綱要設定 {#schema-configuration}

您必須將天氣欄位群組新增到和您在資料流中正在使用的事件資料集相對應的 Experience Platform 綱要。可提供五種欄位群組：

* [!UICONTROL 預報的天氣]
* [!UICONTROL 目前的天氣]
* [!UICONTROL 產品觸發因素]
* [!UICONTROL 相對觸發因素]
* [!UICONTROL 惡劣天氣觸發因素]

## 存取天氣資料 {#access-weather-data}

一旦您取得資料的授權，即可在所有的 Adob&#x200B;&#x200B;e 服務中以各種不同的方式存取。

### Adobe Analytics {#analytics}

在 [!DNL Adobe Analytics] 中，可透過處理規則和您的其餘 [!DNL XDM] 綱要一起對應天氣資料。

您可以在[天氣參考](weather-reference.md)頁面找到可以對應的欄位清單。和所有的 [!DNL XDM] 綱要一樣，索引鍵的首碼為 `a.x`。例如，名為 `weather.current.temperature.farenheit` 的欄位會在 [!DNL Analytics] 中顯示為 `a.x.weather.current.temperature.farenheit`。

![處理規則介面](../assets/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

在 [!DNL Adobe Customer Journey Analytics] 中，可在資料流中指定的資料集中取得天氣資料。只要將天氣屬性[新增到您的綱要中](#prerequisites-prerequisites)，就能將它們[新增到資料檢視](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html) (在 [!DNL Customer Journey Analytics] 中)。

### Real-Time Customer Data Platform {#rtcdp}

天氣資料可在 [Real-Time Customer Data Platform](../../rtcdp/overview.md) 中取得，在區段中使用。天氣資料會附加到事件。

![顯示天氣事件的區段產生器](../assets/data-enrichment/weather/schema-builder.png)

由於天氣狀況多變，Adobe 建議您對區段設定時間限制，如上述範例所示。最後一兩天的寒冷天氣會比 6 個月前的寒冷天氣影響更大。

如需可用的欄位，請參閱[天氣參考](weather-reference.md)。

### Adobe Target {#target}

在 [!DNL Adobe Target] 中，您可以使用天氣資料即時提升個人化。天氣資料會傳遞至 [!DNL Target] (以 [!UICONTROL mBox] 參數的形式)，您可以透過自訂的 [!UICONTROL mBox] 參數進行存取。

![目標對象產生器](../assets/data-enrichment/weather/target-audience-builder.png)

此參數是到特定欄位的 [!DNL XDM] 路徑。如需可用的欄位及其相對應的路徑，請參閱[天氣參考](weather-reference.md)。

## 後續步驟 {#next-steps}

閱讀本文件後，您現在對於如何在各種 Adob&#x200B;&#x200B;e 解決方案中使用天氣資料有了更深入的了解。若要深入了解天氣資料欄位對應，請參閱[欄位對應參考](weather-reference.md)。
