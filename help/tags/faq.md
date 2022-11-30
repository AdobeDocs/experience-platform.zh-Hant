---
title: 標籤疑難排解指南
description: 取得Adobe Experience Platform中標籤常見問題的解答。
exl-id: c06b8e25-4d79-4a11-94da-94ac096b5e33
source-git-commit: b0cc02478273c0b6035488a5d21191ce5cc0e268
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 27%

---

# 標籤疑難排解指南

>[!NOTE]
>
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](./term-updates.md)。

本檔案提供Adobe Experience Platform中標籤常見問題的解答。

## 什麼是標籤？

標籤是Adobe提供的新一代標籤管理功能，內建於Adobe Experience Platform中。 標籤使客戶端能夠：

- 使用稱為&#x200B;*擴充功能*&#x200B;的整合功能，部署用戶端網頁產品
- 動態設定，以更新原生行動應用程式中的用戶端實作
- 一致地在其他廠商和 Adobe 提供的行銷與廣告產品之間擷取、定義、管理和共用資料。

標籤是進階的程式碼和設定傳送系統，會評估條件並執行動作，以有效部署用戶端程式庫和產品。 此外，也提供高度可擴充的整合管理與建置方法，並提供一組完善的API，以供程式化互動。

## 標籤的成本為何？

標籤不需額外付費。 可供任何使用 [!DNL Adobe Experience Cloud] 客戶。

## 聽說現在有外掛程式。那是什麼？

標籤內建在Adobe Experience Platform中，且完全可擴充。 客戶、Adobe合作夥伴、代理及行銷或廣告技術廠商可建立標籤擴充功能，以新增功能或修改現有功能。 此系統可協助合作夥伴和客戶建立、管理及更新自己的整合項目。這只是Adobe開放Adobe Experience Platform的一種方式，讓客戶和合作夥伴能在其上建立產品和業務。 每個人都能更輕鬆地將 Adobe 技術與其他廠商的行銷和廣告技術結合在一起。

## 會隨即推出適用所有協力廠商的擴充功能嗎？

擴充功能已可供Adobe解決方案，以及大量且不斷增加的獨立分析、行銷、廣告和同意廠商及技術使用。 我們會繼續與合作夥伴合作，擴展生態系統。由於技術擁有者可以建立、管理和更新擴充功能，客戶不需仰賴Adobe工程來建立擴充功能。

## 客戶或合作夥伴何時可建立擴充功能？

Tags已開啟幾近全自助的入口網站，擴充功能開發人員可透過該入口網站建立與Adobe Cloud Platform的整合。

我們有許多客戶也選擇使用相同擴充功能開發法，建立自己的私人擴充功能，僅供公司內部使用。

## 標籤是否符合我公司的安全標準？

標籤符為SOC-2和金融服務現代化法案(Gramm-Leach-Bliley Act)。 標籤也提供自行托管的功能。 您可從自己的伺服器或您選擇的CDN提供JavaScript程式庫和行動設定。 對 IT 和安全團隊而言，這可讓您執行自動化的測試、將檔案簽入您自己的版本控制系統，同時完全遵守任何內部生產移轉程序、安全相關規範或其他規定。

## 何時可以移至標籤？

現在是移至標籤的最佳時機。 移轉程式可輕鬆將DTM屬性複製至標籤中。 我們建議您廣泛測試，不過我們已盡量將程序自動化 (無需在頁面上內嵌程式碼變更，也不需自動移轉規則和資料元素)。

## 標籤是否支援單頁應用程式和我慣用的架構？

可以。標籤的功能可讓使用者和擴充功能開發人員在單頁應用程式體驗或Ajax密集型頁面或網站中，有彈性地收集、管理和分送資料。 無論您偏好的開發架構為何均適用，例如 Angular、React.js、Ember、Meteor 等等。

## 標籤是否支援動態資料層？

可以。標籤包含專門監聽動態資料層變更的擴充功能。

## 標籤支援哪些事件類型？

事件類型可透過擴充功能取得。支援的事件類型數量依擴充功能而異。 例如，YouTube 擴充功能包含種四種視訊事件類型：播放、暫停、結束和播放時間。透過擴充功能，標籤可支援任何其他瀏覽器事件類型或合成事件類型，例如特定訪客活動順序。

## 標籤會加速（或減慢）我的網站嗎？

標籤的設計目的，是使用現今的最佳實務，盡可能以最高效率在您的網站上提供和執行行銷和廣告技術。 若正確使用，已證明標籤可比提供類似功能的替代方法來改善網站效能。

## 標籤支援哪些瀏覽器？

標籤的瀏覽器支援：

- [!DNL Chrome] (最新版)
- [!DNL Safari] (最新版)
- [!DNL Firefox] (最新版)
- [!DNL Microsoft Edge] (最新版)
- [!DNL Internet Explorer] (第 10 版及以上版本)
- [!DNL iOS Safari] (最新版)
- [!DNL Android Chrome] (最新版)

標籤應用程式介面的瀏覽器支援：

- [!DNL Chrome] (最新版)
- [!DNL Safari] (最新版)
- [!DNL Firefox] (最新版)
- [!DNL Microsoft Edge] (最新版)

大部分的Adobe用戶端都透過最新版的瀏覽器運用更現代化的Web平台功能，建立更優質的使用者體驗，包括單頁應用程式和互動式Ajax密集型網站與頁面。 隨著大部分的客戶網站改用更現代化的作法，他們需要能支援這些作法的標籤等解決方案。

## 標籤是否適用於原生行動應用程式？

是！標籤現在支援新Adobe Experience Platform的行動屬性和設定 [行動SDK](https://sdkdocs.com) 在原生行動應用程式環境中實作資料收集和傳送。 請參閱[文件](https://sdkdocs.com)以深入了解。

## UI為何說載入我的帳戶時發生錯誤？

如果您收到訊息指出載入帳戶時發生錯誤，表示您的帳戶不屬於任何標籤的產品設定檔。 請參閱 [管理權限](../collection/permissions.md) 了解如何在Adobe Admin Console中設定產品設定檔，以授與UI中資料收集功能的存取權。

## 為何無法在UI中新增任何屬性？

如果您無法在登入UI時建立任何新屬性，表示您的帳戶不屬於具有「管理屬性」權限的產品設定檔。

請參閱 [管理權限](../collection/permissions.md) 了解如何在Adobe Admin Console中設定產品設定檔，以授與「管理屬性」權限。 如需標籤不同權限的詳細資訊，請參閱 [標籤的使用者權限](./ui/administration/user-permissions.md).

## 若我有其他問題該怎麼辦？

若您有其他問題，可在 [Adobe Experience Platform資料收集社群頁面](https://adobe.com/go/launchme) Experience League時，或加入 [社群Slack工作區](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform) 適用於開發人員與技術實作主題。
