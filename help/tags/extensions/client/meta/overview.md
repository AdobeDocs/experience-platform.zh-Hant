---
title: 中繼畫素擴充功能概述
description: 瞭解Adobe Experience Platform中的Meta Pixel標籤擴充功能。
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# [!DNL Meta Pixel]擴充功能概觀

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/)是以JavaScript為基礎的分析工具，可讓您追蹤網站上的訪客活動。 您追蹤的訪客動作（稱為轉換）會傳送至[[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager)，以便用於評估廣告、行銷活動、轉換漏斗等專案的成效。

[!DNL Meta Pixel]標籤延伸可讓您在使用者端標籤資料庫中運用[!DNL Pixel]功能。 本文介紹如何安裝擴充功能，以及在[規則](../../../ui/managing-resources/rules.md)中使用其功能。

## 先決條件

若要使用副檔名，您必須擁有可存取[!DNL Ads Manager]的有效[!DNL Meta]帳戶。 具體來說，您必須[建立新的 [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755)並複製其[!DNL Pixel ID]，才能將擴充功能設定到您的帳戶。 如果您已有[!DNL Meta Pixel]，可以改用其ID。

強烈建議將[!DNL Meta Pixel]與[!DNL Meta Conversions API]搭配使用，分別從使用者端和伺服器端共用及傳送相同的事件，因為這可能有助於復原[!DNL Meta Pixel]未擷取的事件。 如需如何在伺服器端實作中整合事件轉送](../../client/meta/overview.md)的步驟，請參閱[[!DNL Meta Conversions API] 擴充功能的指南。 請注意，您的組織必須擁有[事件轉送](../../../ui/event-forwarding/overview.md)的存取權，才能使用伺服器端擴充功能。

## 安裝擴充功能

若要安裝[!DNL Meta Pixel]擴充功能，請導覽至資料收集UI或Experience Platform UI，然後從左側導覽中選取&#x200B;**[!UICONTROL 標籤]**。 從這裡，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需的屬性後，在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤。 搜尋[!UICONTROL Meta Pixel]卡片，然後選取&#x200B;**[!UICONTROL 安裝]**。

![正在資料收集UI中選取[!UICONTROL Meta Pixel]延伸的[!UICONTROL 安裝]按鈕。](../../../images/extensions/client/meta/install.png)

在出現的設定檢視中，您必須提供您先前複製的[!DNL Pixel] ID，以將擴充功能連結至您的帳戶。 您可以直接將ID貼到輸入中，也可以改為選取現有的資料元素。

>[!TIP]
>
>使用資料元素可讓您根據其他因素（例如組建環境）動態變更所使用的[!DNL Pixel] ID。 如需詳細資訊，請參閱[上針對不同環境使用不同 [!DNL Pixel] ID](#id-data-element)的附錄一節。

您也可以選擇提供事件ID以與擴充功能建立關聯。 這用於刪除[!DNL Meta Pixel]與[!DNL Meta Conversions API]之間的相同事件。 如需詳細資訊，請參閱[!DNL Conversions API]擴充功能的概觀中的[事件重複資料刪除](../../server/meta/overview.md#event-deduplication)一節。

完成後，選取&#x200B;**[!UICONTROL 儲存]**

![擴充功能組態檢視中作為資料元素提供的[!DNL Pixel] ID。](../../../images/extensions/client/meta/configure.png)

擴充功能已安裝，您現在可以在標籤規則中運用其各種動作。

## 設定標籤規則 {#rule}

[!DNL Meta Pixel]接受一組預先定義的[標準事件](https://www.facebook.com/business/help/402791146561655)，每個事件都有自己的內容與接受的屬性。 [!DNL Pixel]擴充功能提供的規則動作與這些事件型別相關，可讓您根據傳送至[!DNL Meta]的事件型別，輕鬆分類及設定事件。

為了示範，本節說明如何建立將頁面檢視事件傳送至[!DNL Meta]的規則。

開始建立新標籤規則，並視需要設定其條件。 選取規則的動作時，請選取&#x200B;**[!UICONTROL Meta Pixel]**&#x200B;作為擴充功能，然後選取&#x200B;**[!UICONTROL 傳送頁面檢視]**&#x200B;作為動作型別。

![正在為資料收集UI中的規則選取[!UICONTROL 傳送頁面檢視]動作型別。](../../../images/extensions/client/meta/select-action.png)

[!UICONTROL 傳送頁面檢視]動作不需要進一步的設定。 選取&#x200B;**[!UICONTROL 保留變更]**&#x200B;以將動作新增至規則設定。 如果您對規則感到滿意，請選取&#x200B;**[!UICONTROL 儲存至程式庫]**。

最後，發佈新標籤[組建](../../../ui/publishing/builds.md)以啟用程式庫的變更。

## 確認[!DNL Meta]正在接收資料

將更新的組建部署到您的網站後，您可以在瀏覽器上產生一些轉換事件，並檢查這些事件是否出現在[[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180)中，以確認資料是否如預期傳送。

## 後續步驟

本指南說明如何使用[!DNL Meta Pixel]標籤延伸將資料傳送至[!DNL Meta]。 如果您也打算將伺服器端事件傳送至[!DNL Meta]，您現在可以繼續安裝並設定[[!DNL Conversions API] 事件轉送擴充功能](../../server/meta/overview.md)。

如需Experience Platform中標籤的詳細資訊，請參閱[標籤總覽](../../../home.md)。

## 附錄：針對不同的環境使用不同的[!DNL Pixel] ID {#id-data-element}

如果您想要在開發或預備環境中測試實作，同時保持生產[!DNL Meta Pixel]分析不變，您可以使用資料元素來根據使用的環境動態選擇適當的[!DNL Pixel] ID。

您可以搭配使用[!UICONTROL 自訂程式碼]資料元素（由[[!UICONTROL 核心]擴充功能](../core/overview.md)提供）與[`turbine`自由變數](../../../extension-dev/turbine.md)來達成此目的。 在資料元素的JavaScript程式碼中，使用`turbine`物件來尋找目前的環境階段，然後根據結果傳回適當的[!DNL Pixel] ID。

下列範例會在生產環境中使用時傳回假的生產ID `exampleProductionKey`，並在使用任何其他環境時傳回不同的ID `exampleTestKey`。 實作此程式碼時，請將每個值取代為您實際的生產和測試[!DNL Pixel] ID。

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
