---
title: 標籤疑難解答指南
description: 獲取有關Adobe Experience Platform標籤的常見問題的答案。
exl-id: c06b8e25-4d79-4a11-94da-94ac096b5e33
source-git-commit: a99046cc7df18d53b068c679ab07f5f9dd8eff0a
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 27%

---

# 標籤疑難解答指南

>[!NOTE]
>
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](./term-updates.md)。

本文檔提供有關Adobe Experience Platform標籤的常見問題的解答。

## 什麼是標籤？

標籤是Adobe提供的下一代標籤管理功能，內置於Adobe Experience Platform。 標籤使客戶端能夠：

- 使用稱為&#x200B;*擴充功能*&#x200B;的整合功能，部署用戶端網頁產品
- 動態設定，以更新原生行動應用程式中的用戶端實作
- 一致地在其他廠商和 Adobe 提供的行銷與廣告產品之間擷取、定義、管理和共用資料。

標籤是一種高級代碼和配置交付系統，它評估條件並執行操作以高效、高效地部署客戶端庫和產品。 它們還提供了一種高度可擴展的整合管理和構建方法，並具有一組強健的API用於寫程式交互。

## 標籤的成本是多少？

標籤不額外收費。 它們可供任何 [!DNL Adobe Experience Cloud] 客戶。

## 聽說現在有外掛程式。那是什麼？

標籤內置在Adobe Experience Platform中，並且完全可擴展。 客戶、Adobe合作夥伴、代理、營銷或廣告技術供應商可以構建一個標籤擴展，添加新功能或修改現有功能。 此系統可協助合作夥伴和客戶建立、管理及更新自己的整合項目。這只是Adobe開放Adobe Experience Platform的一種方式，這樣客戶和合作夥伴就可以在其上構建產品和業務。 每個人都能更輕鬆地將 Adobe 技術與其他廠商的行銷和廣告技術結合在一起。

## 會隨即推出適用所有協力廠商的擴充功能嗎？

Adobe解決方案以及大量且不斷增加的獨立分析、營銷、廣告和同意供應商和技術已經可以擴展。 我們會繼續與合作夥伴合作，擴展生態系統。由於擴展可由技術所有者構建、管理和更新，因此客戶不必等待Adobe工程來構建它們。

## 客戶或合作夥伴何時可建立擴充功能？

標籤已經開啟了它的實際自助服務門戶，擴展開發人員可以使用該門戶構建與Adobe Cloud Platform的整合。

我們有許多客戶也選擇使用相同擴充功能開發法，建立自己的私人擴充功能，僅供公司內部使用。

## 標籤是否符合我公司的安全標準？

標籤為SOC-2和Gramm-Leach-Bliley Act。 標籤還提供自我承載的能力。 JavaScript庫和移動配置可以從您自己的伺服器或您選擇的CDN中提供。 對 IT 和安全團隊而言，這可讓您執行自動化的測試、將檔案簽入您自己的版本控制系統，同時完全遵守任何內部生產移轉程序、安全相關規範或其他規定。

## 何時可以移到標籤？

現在是轉移到標籤的最佳時機。 遷移過程使DTM屬性輕鬆複製到標籤中。 我們建議您廣泛測試，不過我們已盡量將程序自動化 (無需在頁面上內嵌程式碼變更，也不需自動移轉規則和資料元素)。

## 標籤是否支援單頁應用和我最喜愛的框架？

可以。標籤具有使用戶和擴展開發人員能夠在單頁應用程式體驗或Ajax繁重的頁面或站點中收集、管理和分發資料的靈活性。 無論您偏好的開發架構為何均適用，例如 Angular、React.js、Ember、Meteor 等等。

## 標籤是否支援動態資料層？

可以。標籤包括專門偵聽動態資料層更改的擴展。

## 標籤支援哪些事件類型？

事件類型可透過擴充功能取得。支援的事件類型的數量因擴展而異。 例如，YouTube 擴充功能包含種四種視訊事件類型：播放、暫停、結束和播放時間。通過擴展，標籤可以支援任何其他瀏覽器事件類型或合成事件類型，如特定訪問者活動序列。

## 標籤會加快（還是減慢）我的網站？

標籤旨在利用當今的最佳實踐，盡可能高效地在您的網站上提供和運行營銷和廣告技術。 在正確使用時，已證明標籤比提供類似功能的替代方法能夠改善網站的效能。

## 哪些瀏覽器支援標籤？

瀏覽器支援標籤：

- [!DNL Chrome] (最新版)
- [!DNL Safari] (最新版)
- [!DNL Firefox] (最新版)
- [!DNL Microsoft Edge] (最新版)
- [!DNL Internet Explorer] (第 10 版及以上版本)
- [!DNL iOS Safari] (最新版)
- [!DNL Android Chrome] (最新版)

瀏覽器支援標籤應用程式介面：

- [!DNL Chrome] (最新版)
- [!DNL Safari] (最新版)
- [!DNL Firefox] (最新版)
- [!DNL Microsoft Edge] (最新版)

大多數Adobe客戶端都利用當前瀏覽器中更現代的Web平台功能來建立更好的用戶體驗，包括單頁應用程式和繁重Ajax的互動式網站和頁面。 隨著大多數客戶在其站點上轉向更現代的方法，他們需要一種像標籤這樣的解決方案來支援這些方法。

## 標籤在本機移動應用上有效嗎？

是！標籤現在支援新Adobe Experience Platform的移動屬性和配置 [移動SDK](https://sdkdocs.com) 在本機移動應用環境中實現資料收集和傳遞。 請參閱[文件](https://sdkdocs.com)以深入了解。

## UI為什麼說載入我的帳戶時出錯？

如果您收到一條消息，說載入帳戶時出錯，則表示您的帳戶不屬於任何標籤產品配置檔案。 請參閱上的指南 [管理權限](../rtcdp-connections/permissions.md) 瞭解如何在Adobe Admin Console配置產品配置檔案以授予對資料收集UI的訪問權限。

## 為什麼無法在UI中添加任何屬性？

如果登錄到資料收集UI時無法建立新屬性，則表示您的帳戶不屬於具有管理屬性權限的產品配置檔案。

請參閱上的指南 [管理權限](../rtcdp-connections/permissions.md) 瞭解如何在Adobe Admin Console配置產品配置檔案以授予「管理屬性」權限。 有關標籤不同權限的詳細資訊，請參閱 [標籤的用戶權限](./ui/administration/user-permissions.md)。

## 若我有其他問題該怎麼辦？

如果你有其他問題，你可以問 [Adobe Experience Platform資料收集社區頁](https://adobe.com/go/launchme) Experience League，或加入 [標籤開發商官方Slack小組](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform)。
