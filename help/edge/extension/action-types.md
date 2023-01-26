---
title: Adobe Experience Platform Web SDK擴充功能中的動作類型
description: 了解Adobe Experience Platform Web SDK標籤擴充功能提供的不同動作類型。
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 1b0f1e2e1625f6994a6e09bd086e4b63a3e8d4ab
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---

# 動作類型

設定 [Adobe Experience Platform Web SDK標籤擴充功能](web-sdk-extension-configuration.md)，設定動作類型。

本頁面說明可用的動作類型。


## 傳送事件

傳送事件至Adobe [!DNL Experience Platform] 讓Adobe Experience Platform能夠收集您傳送的資料，並對該資訊採取行動。 選取例項（如果您有多個例項）。 您可以在 **[!UICONTROL XDM資料]** 欄位。 使用符合XDM結構的JSON物件。 可在您的頁面上，或透過 **[!UICONTROL 自訂程式碼]** **[!UICONTROL 資料元素]**.

「傳送事件」動作類型中還有一些其他欄位，視您的實作而定。 請注意，這些欄位都是選填欄位。

- **類型：** 此欄位可讓您指定要記錄在XDM架構中的事件類型。 請參閱 [檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) 以取得預設事件類型的詳細資訊。
- **資料：** 可使用此欄位傳送不符合XDM架構的資料。 如果您嘗試更新Adobe Target設定檔或傳送Target Recommendations屬性，此欄位就十分實用。 如需範例，請檢視 [檔案](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en).<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **資料集ID:** 如果您需要將資料傳送至資料流中指定之資料以外的資料集，可以在此處指定該資料集ID。
- **文檔將卸載：** 如果您想要確保即使使用者離開頁面進行導覽，事件仍可送達伺服器，請檢查 **[!UICONTROL 文檔將卸載]** 核取方塊。 這可讓事件到達伺服器，但會忽略回應。
- **呈現視覺個人化決策：** 如果您想在頁面上呈現個人化內容，請核取 **[!UICONTROL 轉譯視覺個人化決策]** 核取方塊。 如有必要，還可以指定決策範圍和/或曲面。 請參閱 [個人化檔案](../personalization/rendering-personalization-content.md#automatically-rendering-content) 以取得轉譯個人化內容的詳細資訊。

## 設定同意

在您收到使用者的同意後，必須使用「設定同意」動作類型將此同意傳達至Adobe Experience Platform Web SDK。 目前支援「Adobe」和「IAB TCF」等兩種標準。請參閱 [支援客戶同意偏好設定](../consent/supporting-consent.md). 使用Adobe2.0版時，僅支援資料元素值。 您需要建立解析至同意物件的資料元素。

此動作中也提供選用欄位，供您包含「身分對應」，以便在收到同意後同步身分。 同步在同意設為「擱置中」或「退出」時相當實用，因為同意呼叫可能是第一個觸發的呼叫。

## 重設事件合併 ID

如果您想在頁面上重設事件合併ID，可透過此動作執行。 若要重設ID，請選取您要重設的合併ID，並視需要觸發動作。

## 接下來

設定動作後， [設定資料元素類型](data-element-types.md).
