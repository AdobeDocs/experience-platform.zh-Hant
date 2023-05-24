---
title: Adobe Experience PlatformWeb SDK擴展中的操作類型
description: 瞭解Adobe Experience PlatformWeb SDK標籤擴展提供的不同操作類型。
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 2%

---


# 動作類型

配置 [Adobe Experience PlatformWeb SDK標籤擴展](web-sdk-extension-configuration.md)，必須配置操作類型。

此頁介紹了支援的操作類型 [Adobe Experience PlatformWeb SDK標籤擴展](web-sdk-extension-configuration.md)。

## 發送事件 {#send-event}

將事件發送到Adobe [!DNL Experience Platform] 這樣Adobe Experience Platform就能收集你發送的資料，並根據這些資訊採取行動。 選擇一個實例（如果您有多個實例）。 您要發送的任何資料都可以在 **[!UICONTROL XDM資料]** 的子菜單。 使用符合XDM架構結構的JSON對象。 此對象可以在您的頁面上建立，也可以通過 **[!UICONTROL 自定義代碼]** **[!UICONTROL 資料元素]**。

「發送事件」操作類型中還有一些其它欄位，這些欄位可能也會根據您的實施情況而有用。 請注意，這些欄位都是可選的。

- **類型：** 此欄位允許您指定將記錄在XDM架構中的事件類型。 查看 [文檔](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) 的子菜單。
- **資料：** 可以使用此欄位發送與XDM架構不匹配的資料。 如果您試圖更新Adobe Target配置檔案或發送目標Recommendations屬性，則此欄位非常有用。 有關示例，請查看 [文檔](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=zh-Hant)。<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **資料集ID:** 如果您需要將資料發送到資料流中指定的資料集以外的資料集，則可以在此處指定該資料集ID。
- **文檔將卸載：** 如果希望確保事件到達伺服器，即使用戶從頁面導航出去，請檢查 **[!UICONTROL 將卸載文檔]** 複選框。 這允許事件到達伺服器，但忽略響應。
- **呈現可視個性化決定：** 如果要在頁面上呈現個性化內容，請檢查 **[!UICONTROL 呈現可視個性化決定]** 複選框。 如有必要，還可以指定決策範圍和/或曲面。 查看 [個性化文檔](../personalization/rendering-personalization-content.md#automatically-rendering-content) 的子菜單。

## 設定同意 {#set-consent}

在您收到用戶的同意後，必須使用「設定同意」操作類型將此同意傳達給Adobe Experience PlatformWeb SDK。 目前支援「Adobe」和「IAB TCF」等兩種標準。請參閱 [支援客戶同意首選項](../consent/supporting-consent.md)。 使用Adobe2.0版時，僅支援資料元素值。 您需要建立一個解析為同意對象的資料元素。

在此操作中，還為您提供了一個可選欄位以包含身份映射，以便在收到同意後可以同步身份。 同步在同意配置為「待處理」或「出現」時非常有用，因為同意呼叫可能是第一個呼叫觸發。

## 重置事件合併ID {#reset-event-merge-id}

如果要在頁面上重置事件合併ID，可以通過此操作進行重置。 要重置ID，請選擇要重置的合併ID，然後根據需要啟動操作。

## (Beta)更新變數 {#update-variable}

>[!IMPORTANT]
>
>這是當前的測試版功能，可能會發生更改。 將來的版本可能包含中斷更改。

使用此操作可以修改XDM對象作為事件的結果。 此操作旨在構建一個以後可以從 **[!UICONTROL 發送事件]** 操作，記錄事件XDM對象。

要使用此操作類型，必須已定義 [變數](data-element-types.md#variable) 資料元素。 選擇要修改的變數資料元素後，將出現一個編輯器，類似於 [XDM對象](data-element-types.md#xdm-object) 資料元素。

![](./assets/update-variable.png)

用於編輯器的XDM架構是在 [!UICONTROL 變數] 資料元素。 通過按一下左側樹中的一個屬性，然後修改右側的值，可以設定對象的一個或多個屬性。例如，在下面的螢幕快照中，productedBy屬性將設定為資料元素「由資料元素生成」。

![](./assets/update-variable-set-property.png)

更新變數操作中的編輯器與XDM對象資料元素中的編輯器之間有一些差異。 首先，更新變數操作具有標有「xdm」的根級別項。 如果按一下此項，則可以指定用於設定整個對象的資料元素。 其次，更新變數操作具有用於從xdm對象中清除資料的複選框。 按一下左側的一個屬性，然後選中右側的複選框以清除該值。 這將在設定變數的任何值之前清除當前值。

## 後續步驟 {#next-steps}

閱讀這篇文章後，您應該對如何配置操作有更好的瞭解。 接下來，閱讀有關 [配置資料元素類型](data-element-types.md)。
