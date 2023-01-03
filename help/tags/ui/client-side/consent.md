---
title: 部署JavaScript標籤以管理客戶同意
description: 了解如何在Adobe Experience Platform中管理各種Adobe解決方案的客戶選擇加入和選擇退出訊號。
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: 3bb0fc7b2807889d0a759e81c8ff728de3c0cbde
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 78%

---

# 部署JavaScript標籤以管理客戶同意

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](../../term-updates.md)。

一般資料保護規範(GDPR)等法律隱私權法規要求公司必須能夠管理其使用者的同意聲明。 Adobe客戶可能會要求Adobe者選擇加入，才能針對任何特定訪客執行客戶解決方案。 訪客應該要能管理自己的選擇加入和選擇退出狀態。

Adobe Experience Cloud客戶對這些需求需要執行各種不同的實作。 有些使用企業級同意聲明管理工具，有些則建置自己的工具。

Adobe Experience Platform擴充功能開發人員使用擴充功能和規則產生器，以定義選擇加入和選擇退出解決方案。

本文件包含有關如何在獲得同意前阻止 Adobe 標籤引發的資訊。

## Advertising Cloud

Adobe Experience Platform未引發 [!DNL Advertising Cloud] 自動。 只有在您明確指定規則動作時，才會引發 [!DNL Advertising Cloud]。使用規則條件來判斷要在何時引發以及要引發的行為。例如，若要使用 Cookie 判斷選擇加入狀態，請設定資料元素以讀取該 Cookie 並將其用作規則中的條件，以判斷何時引發「追蹤轉換」動作。

整合同意聲明管理工具 (例如 OneTrust) 後可設定及追蹤客戶的同意 Cookie，這些之後可在規則產生器中使用。

## Analytics

在 [!DNL Analytics] 擴充功能之組態設定的 Link Tracking 區段中，確認&#x200B;*未選取*&#x200B;下列項目：

* 追蹤下載連結
* 追蹤對外連結

未選取這些設定時，Platform不會引發 [!DNL Adobe Analytics] 自動。 只有在您明確指定規則動作時，[!DNL Analytics] 才會引發。使用規則條件來判斷要在何時引發以及要引發的行為。例如，若要使用 Cookie 判斷選擇加入狀態，請設定資料元素以讀取該 Cookie 並將其用作規則中的條件，以判斷何時引發「傳送信標」動作。

另外，您可以考慮使用 [Adobe 選擇加入物件](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html)，搭配您的同意聲明管理平台，控制此標籤的引發機制。

整合同意聲明管理工具 (例如 OneTrust) 後可設定及追蹤客戶的同意 Cookie，這些之後可在規則產生器中使用。

## Audience Manager

若放置於客戶頁面上，DIL 目前已設為自動引發。請考慮使用 [Adobe 選擇加入物件](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html)，搭配您的同意聲明管理平台，控制此標籤的引發機制。

[!DNL Adobe] 建議您在 [!DNL Analytics] 內使用伺服器端轉送。

## Experience Cloud ID

[!DNL Experience Cloud ID] 現在會自動在客戶頁面上引發。

請考慮使用 [Adobe 選擇加入物件](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html)，搭配您的同意聲明管理平台，控制此標籤的引發機制。

## Target

Adobe Experience Platform未引發 [!DNL Target] 自動。 只有在您明確指定規則動作時，[!DNL Target] 才會引發。使用規則條件來判斷要在何時引發以及要引發的行為。例如，若要使用 Cookie 判斷選擇加入狀態，請設定資料元素以讀取該 Cookie 並將其用作規則中的條件，以判斷何時引發「載入 [!DNL Target]」動作。

另外，您可以考慮使用 [Adobe 選擇加入物件](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html)，搭配您的同意聲明管理平台，控制此標籤的引發機制。

整合同意聲明管理工具 (例如 OneTrust) 後可設定及追蹤客戶的同意 Cookie，這些之後可在規則產生器中使用。
