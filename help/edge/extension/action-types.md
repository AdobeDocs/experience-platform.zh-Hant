---
title: Adobe Experience Platform網頁SDK擴充功能中的動作類型
description: 瞭解Adobe Experience Platform LaunchAdobe Experience Platform網頁SDK擴充功能提供的不同動作類型。
translation-type: tm+mt
source-git-commit: ff261c507d310b8132912680b6ddd1e7d5675d08
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 6%

---


# 動作類型

為[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)配置[Adobe Experience PlatformWeb SDK擴展](web-sdk-extension.md)後，請配置您的操作類型。

本頁介紹可用的操作類型。

## 傳送事件

傳送事件至Adobe[!DNL Experience Platform]，讓Adobe Experience Platform可以收集您傳送的資料，並對該資訊採取行動。 選取例項（如果您有多個例項）。 如果事件發生在頁面載入的開始或在單一頁面應用程式的檢視變更期間，請選取&#x200B;**[!UICONTROL 在檢視的開始時發生]**。

您要傳送的任何資料都可在&#x200B;**[!UICONTROL XDM資料]**&#x200B;欄位中傳送。 使用符合XDM結構的JSON物件。 此物件可在您的頁面上建立，或透過&#x200B;**[!UICONTROL 自訂代碼]** **[!UICONTROL 資料元素]**&#x200B;建立。

## 設定同意

在您收到使用者的同意後，必須使用「設定同意」動作類型將此同意傳達至Adobe Experience Platform網頁SDK。 目前支援「Adobe」和「IAB TCF」等兩種標準。請參閱[支援客戶同意首選項](../consent/supporting-consent.md)。 使用Adobe2.0版時，僅支援資料元素值。 您將需要建立可解析至同意物件的資料元素。

在此動作中，您也會收到選填欄位，以包含身分圖，以便在收到同意後同步身分。 同步在同意設定為「擱置中」或「退出」時很有用，因為同意呼叫可能是第一個要觸發的呼叫。

## 重設事件合併 ID

如果您想要重設頁面上的事件合併ID，則可透過此動作執行。 若要重設ID，請選取您要重設的合併ID，並視需要觸發動作。

## 下一步

設定動作類型後，[設定您的資料元素類型](data-element-types.md)。