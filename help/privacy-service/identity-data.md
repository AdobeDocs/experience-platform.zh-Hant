---
keywords: Experience Platform；首頁；熱門主題；ECID;ecid
solution: Experience Platform
title: 隱私請求的標識資料
description: 本文檔提供有關如何配置資料操作和利用Adobe技術以有效檢索客戶隱私請求的適當身份資訊的一般指導。
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---

# 隱私請求的標識資料

為了Adobe Experience Platform [!DNL Privacy Service] 要處理客戶對其私有資料的請求（包括訪問、刪除或選擇退出銷售請求），必須提供唯一標識符，將特定客戶與其在您啟用Adobe Experience Cloud的應用程式中儲存的私有資料連結起來。 [!DNL Privacy Service] 然後使用這些標識符來收集儲存在以下位置的所有資料： [!DNL Experience Cloud]，並根據客戶的要求進行處理。

本文檔提供有關如何配置資料操作和利用Adobe技術以有效檢索客戶隱私請求的適當身份資訊的一般指導。

## 標識和命名空間

當客戶可以通過多個不同渠道與您的品牌進行交互時，協調從這些多次交互中記錄的不同標識符可能會非常困難。 這反過來又會使您難以確定哪些資料屬於您的特定人員 [!DNL Experience Cloud] 應用程式。

例如，在處理客戶資料請求時 [!DNL Privacy Service]，標識可以表示在Adobe控制域下設定的cookie值、在第三方域下並與Adobe共用的cookie值，或您在組織內明確定義的自定義標識符。

因此，需要將每個身份發送到 [!DNL Privacy Service] 帶有一個命名空間，該命名空間通過將標識值與其源系統相關聯而提供上下文。 命名空間可以表示一個通用概念，如電子郵件地址（「電子郵件」），或將標識與特定應用程式(如Adobe Advertising CloudID(「AdCloud」)或Adobe TargetID(「TNTID」))關聯。

Adobe Experience Platform標識服務維護全局定義和用戶定義的標識命名空間的儲存。 有關命名空間的詳細資訊，請參見 [標識命名空間概述](../identity-service/namespaces.md)。 用於常用於的標準命名空間和命名空間限定符的清單 [!DNL Privacy Service]，請參見 [附錄部分](api/appendix.md) 的上界。

## ECID和選擇加入服務

Adobe Experience Cloud [!DNL Identity Service] 用作 [!DNL Experience Cloud]，並為每個站點訪問者分配一個唯一的持久ID。 的 [!DNL Experience Cloud] ID(ECID)通過使用第一方cookie跟蹤客戶的活動，可以跨多個應用程式唯一標識設備，並允許您標識同一站點訪問者及其位於不同位置的資料 [!DNL Experience Cloud] 應用程式。 查看 [Experience CloudIdentity Service概述](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) 的子菜單。

選擇加入服務， [!DNL Experience Cloud Identity Service]，允許您在應用程式上設定協定，以便訪問者確定您是否可以在訪問者設備或瀏覽器上設定cookie。 有關選擇加入服務的更多詳細資訊，包括如何為您的應用程式設定服務，請參閱 [選擇服務文檔](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hant)。

一旦為站點訪問者分配了ECID，您就可以利用Adobe [!DNL Privacy JavaScript Library] 以檢索這些ID以用於隱私請求，如下一節所述。

## [!DNL Privacy JS Library]

的 [!DNL Adobe Privacy JavaScript Library] 提供了幾個功能，允許您檢索和刪除儲存在瀏覽器中的客戶身份。 該庫可配置為從包括ECID在內的多個Adobe應用程式檢索身份資訊。 通過使用回調或承諾，可以以寫程式方式處理成功檢索到的ID，並將它們發送到 [!DNL Privacy Service] API。

有關 [!DNL Privacy JS Library]，包括幾個常用案例的代碼示例，請參閱 [隱私JS庫概述](js-library.md)。

## 後續步驟

本文檔簡要概述了檢索客戶身份資料以用於隱私請求所涉及的核心概念。 建議您查看每節中提供的文檔連結，以瞭解有關這些概念和服務的詳細資訊。 有關如何將檢索到的ID發送到 [!DNL Privacy Service] 有關建立訪問、刪除或選擇退出銷售請求的資訊，請參閱 [Privacy ServiceAPI指南](api/overview.md)。
