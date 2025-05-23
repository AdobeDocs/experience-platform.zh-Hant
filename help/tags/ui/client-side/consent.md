---
title: 部署JavaScript標籤以管理客戶同意
description: 瞭解如何在Adobe Experience Platform中針對各種Adobe解決方案管理客戶選擇加入和選擇退出訊號。
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 79%

---

# 部署JavaScript標籤以管理客戶同意

>[!NOTE]
>
>Adobe Experience Platform Launch 已進行品牌重塑，現在是 Adobe Experience Platform 中的一套資料彙集技術。 因此，這些產品文件都推出多項幾術語變更。如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

一般資料保護規範(GDPR)等隱私權法規要求公司必須能夠管理其使用者的同意宣告。 Adobe客戶在為任何特定訪客執行Adobe解決方案之前，可能會要求訪客選擇加入。 訪客應該要能管理自己的選擇加入和選擇退出狀態。

Adobe Experience Cloud客戶對這些需求要求進行各種不同實施。 有些使用企業級同意聲明管理工具，有些則建置自己的工具。

Adobe Experience Platform擴充功能開發人員可使用擴充功能及規則產生器，以定義選擇加入和選擇退出解決方案。

本文件包含有關如何在獲得同意前阻止 Adobe 標籤引發的資訊。

## Advertising Cloud

Adobe Experience Platform不會自動引發[!DNL Advertising Cloud]。 只有在您明確指定規則動作時，才會引發 [!DNL Advertising Cloud]。使用規則條件來判斷要在何時引發以及要引發的行為。例如，若要使用 Cookie 判斷選擇加入狀態，請設定資料元素以讀取該 Cookie 並將其用作規則中的條件，以判斷何時引發「追蹤轉換」動作。

整合同意聲明管理工具 (例如 OneTrust) 後可設定及追蹤客戶的同意 Cookie，這些之後可在規則產生器中使用。

## Analytics

在 [!DNL Analytics] 擴充功能之組態設定的 Link Tracking 區段中，確認&#x200B;*未選取*&#x200B;下列項目：

* 追蹤下載連結
* 追蹤對外連結

未選取這些設定時，Experience Platform不會自動引發[!DNL Adobe Analytics]。 只有在您明確指定規則動作時，[!DNL Analytics] 才會引發。使用規則條件來判斷要在何時引發以及要引發的行為。例如，若要使用 Cookie 判斷選擇加入狀態，請設定資料元素以讀取該 Cookie 並將其用作規則中的條件，以判斷何時引發「傳送信標」動作。

另外，您可以考慮使用 [Adobe 選擇加入物件](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hant)，搭配您的同意聲明管理平台，控制此標籤的引發機制。

整合同意聲明管理工具 (例如 OneTrust) 後可設定及追蹤客戶的同意 Cookie，這些之後可在規則產生器中使用。

## Audience Manager

若放置於客戶頁面上，DIL 目前已設為自動引發。請考慮使用 [Adobe 選擇加入物件](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hant)，搭配您的同意聲明管理平台，控制此標籤的引發機制。

[!DNL Adobe] 建議您在 [!DNL Analytics] 內使用伺服器端轉送。

## Experience Cloud ID

[!DNL Experience Cloud ID] 現在會自動在客戶頁面上引發。

請考慮使用 [Adobe 選擇加入物件](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hant)，搭配您的同意聲明管理平台，控制此標籤的引發機制。

## Target

Adobe Experience Platform不會自動引發[!DNL Target]。 只有在您明確指定規則動作時，[!DNL Target] 才會引發。使用規則條件來判斷要在何時引發以及要引發的行為。例如，若要使用 Cookie 判斷選擇加入狀態，請設定資料元素以讀取該 Cookie 並將其用作規則中的條件，以判斷何時引發「載入 [!DNL Target]」動作。

另外，您可以考慮使用 [Adobe 選擇加入物件](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hant)，搭配您的同意聲明管理平台，控制此標籤的引發機制。

整合同意聲明管理工具 (例如 OneTrust) 後可設定及追蹤客戶的同意 Cookie，這些之後可在規則產生器中使用。
