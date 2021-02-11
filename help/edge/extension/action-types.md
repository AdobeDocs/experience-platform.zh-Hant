---
title: 平台網頁SDK擴充功能動作類型
description: Adobe Experience Platform Launch中的Adobe Experience Platform Web SDK擴充功能動作類型
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 54%

---


# 動作類型

在您為[Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html)設定[Adobe Experience Platform Web SDK擴充功能](web-sdk-extension.md)後，請設定您的動作類型。

本頁介紹可用的操作類型。

## 傳送事件

傳送事件至Adobe [!DNL Experience Platform]，讓Adobe Experience Platform可收集您傳送的資料，並據此採取行動。 如果有多個例項，則必須選取例項。如果事件發生在頁面載入的開始或在單一頁面應用程式的檢視變更期間，請選取&#x200B;**[!UICONTROL 在檢視的開始時發生]**。

您要傳送的任何資料都可在&#x200B;**[!UICONTROL XDM資料]**&#x200B;欄位中傳送。 這應為符合 XDM 結構的 JSON 物件。此物件可在您的頁面上建立，或透過&#x200B;**[!UICONTROL 自訂代碼]** **[!UICONTROL 資料元素]**&#x200B;建立。

## 設定同意

在您獲得使用者同意後，必須將此資訊傳達給Adobe Experience Platform Web SDK。 您可以使用「設定同意」動作類型來執行此動作。目前支援「Adobe」和「IAB TCF」等兩種標準。如果使用 Adobe 標準，目前您可將同意宣告設為「加入」或「退出」，或者也可使用資料元素來提供。如果使用 IAB TCF 標準，請提供要使用的版本和值，以及其他 GDPR 相關資訊。

在此動作中，系統也會提供選填欄位，供您加入身分對應，以便在收到同意後同步身分資料。同意設為「待處理」時，這項功能可能相當實用，因為同意呼叫很可能是第一個要觸發的呼叫。

## 重設事件合併 ID

如果您要重設頁面上的事件合併 ID，可透過此動作來執行。若要重設 ID，您必須選取要重設的合併 ID，並視需求觸發動作。

## 下一步

設定動作類型後，[設定您的資料元素類型](data-element-types.md)。