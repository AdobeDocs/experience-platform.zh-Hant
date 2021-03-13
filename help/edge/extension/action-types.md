---
title: Adobe Experience Platform網頁SDK擴充功能中的動作類型
description: 瞭解Adobe Experience Platform LaunchAdobe Experience Platform網頁SDK擴充功能提供的不同動作類型。
solution: Experience Platform
feature: Web SDK
translation-type: tm+mt
source-git-commit: 9ce6dd5a290b55da04f4ae185cab96c120777775
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 4%

---


# 動作類型

為[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)配置[Adobe Experience PlatformWeb SDK擴展](web-sdk-extension.md)後，請配置您的操作類型。

本頁介紹可用的操作類型。

## 傳送事件

傳送事件至Adobe[!DNL Experience Platform]，讓Adobe Experience Platform可以收集您傳送的資料，並對該資訊採取行動。 選取例項（如果您有多個例項）。 您要傳送的任何資料都可在&#x200B;**[!UICONTROL XDM資料]**&#x200B;欄位中傳送。 使用符合XDM結構的JSON物件。 此物件可在您的頁面上建立，或透過&#x200B;**[!UICONTROL 自訂代碼]** **[!UICONTROL 資料元素]**&#x200B;建立。

「傳送事件」動作類型中還有一些其他欄位，視您的實作而定，這些欄位也會很有用。 請注意，這些欄位都是選用的。

- **類型：** 此欄位可讓您指定要記錄在XDM架構中的事件類型。如需預設事件類型的詳細資訊，請參閱[檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api)。
- **合併ID:** 如果您想要為事件指 [定](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/merging-event-data.html?lang=en#fundamentals) 合併ID，可在此欄位中執行此動作。請注意，下游解決方案目前無法合併您的事件資料。
- **資料集ID:** 如果您需要將資料傳送至邊緣設定中指定之資料集以外的資料集，您可以在此處指定該資料集ID。
- **文檔將卸載：** 如果您希望確保事件到達伺服器，即使用戶從頁面導航離開，請選中「文檔將卸載」 **[!UICONTROL 複選框]** 。這可讓事件觸及伺服器，但會忽略回應。
- **呈現視覺個人化決策：** 如果您想要在頁面上呈現個人化內容，請勾選「呈現視覺個人化 **[!UICONTROL 決策」]** 核取方塊。您也可以視需要指定決策範圍。 如需有關轉譯個人化內容的詳細資訊，請參閱[個人化檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content)。

## 設定同意

在您收到使用者的同意後，必須使用「設定同意」動作類型將此同意傳達至Adobe Experience Platform網頁SDK。 目前支援「Adobe」和「IAB TCF」等兩種標準。請參閱[支援客戶同意首選項](../consent/supporting-consent.md)。 使用Adobe2.0版時，僅支援資料元素值。 您將需要建立可解析至同意物件的資料元素。

在此動作中，您也會收到選填欄位，以包含身分圖，以便在收到同意後同步身分。 同步在同意設定為「擱置中」或「退出」時很有用，因為同意呼叫可能是第一個呼叫觸發。

## 重設事件合併 ID

如果您想要重設頁面上的事件合併ID，則可透過此動作執行。 若要重設ID，請選取您要重設的合併ID，並視需要觸發動作。

## 下一步

設定動作後，[設定您的資料元素類型](data-element-types.md)。
