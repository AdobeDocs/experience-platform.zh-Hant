---
title: Adobe Experience Platform網頁SDK擴充功能中的動作類型
description: 瞭解Adobe Experience Platform LaunchAdobe Experience Platform網頁SDK擴充功能提供的不同動作類型。
translation-type: tm+mt
source-git-commit: 2a0ae9541a8bb2bb985d43a402d0842e73b23c81
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 18%

---


# 動作類型

為[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)配置[Adobe Experience PlatformWeb SDK擴展](web-sdk-extension.md)後，請配置您的操作類型。

本頁介紹可用的操作類型。

## 傳送事件

傳送事件至Adobe[!DNL Experience Platform]，讓Adobe Experience Platform可以收集您傳送的資料，並對該資訊採取行動。 選取例項（如果您有多個例項）。 如果事件發生在頁面載入的開始或在單一頁面應用程式的檢視變更期間，請選取&#x200B;**[!UICONTROL 在檢視的開始時發生]**。

您要傳送的任何資料都可在&#x200B;**[!UICONTROL XDM資料]**&#x200B;欄位中傳送。 使用符合XDM結構的JSON物件。 此物件可在您的頁面上建立，或透過&#x200B;**[!UICONTROL 自訂代碼]** **[!UICONTROL 資料元素]**&#x200B;建立。

## 設定同意

在您收到使用者的同意後，必須使用「設定同意」動作類型將此同意傳達至Adobe Experience Platform網頁SDK。 目前支援「Adobe」和「IAB TCF」等兩種標準。如果使用 Adobe 標準，目前您可將同意宣告設為「加入」或「退出」，或者也可使用資料元素來提供。如果使用 IAB TCF 標準，請提供要使用的版本和值，以及其他 GDPR 相關資訊。

在此動作中，您也會收到選填欄位，以包含身分圖，以便在收到同意後同步身分。 同步在同意設定為「擱置中」時很有用，因為同意呼叫很可能是第一個要觸發的呼叫。

## 重設事件合併 ID

如果您想要重設頁面上的事件合併ID，則可透過此動作執行。 若要重設ID，請選取您要重設的合併ID，並視需要觸發動作。

## 下一步

設定動作類型後，[設定您的資料元素類型](data-element-types.md)。