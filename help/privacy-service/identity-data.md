---
keywords: Experience Platform;home；熱門主題；ECID;ecid
solution: Experience Platform
title: 隱私權要求的身分資料
topic-legacy: overview
description: 本檔案提供如何設定資料作業和運用Adobe技術，以有效擷取適當的客戶隱私權要求身分資訊的一般指引。
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---

# 隱私權要求的身分資料

為讓Adobe Experience Platform[!DNL Privacy Service]處理客戶對其私人資料的要求（包括存取、刪除或選擇退出銷售要求），必須提供唯一識別碼，將特定客戶連結至您啟用Adobe Experience Cloud的應用程式中儲存的私人資料。 [!DNL Privacy Service] 然後使用這些識別碼來收集客戶識別碼下儲存的所有資料 [!DNL Experience Cloud]，並根據客戶的要求加以處理。

本檔案提供如何設定資料作業和運用Adobe技術，以有效擷取適當的客戶隱私權要求身分資訊的一般指引。

## 身分與名稱空間

當客戶可以透過數個不同通道與您的品牌互動時，要協調從這些眾多互動中記錄的不同識別碼可能非常困難。 這反過來又會讓您難以判斷哪些資料屬於[!DNL Experience Cloud]應用程式中的特定人員。

例如，在[!DNL Privacy Service]中處理客戶資料請求時，身分可代表在Adobe控制網域下設定的Cookie值、在協力廠商網域下並與Adobe共用的Cookie值，或您在IMS組織內明確定義的自訂識別碼。

因此，每個傳送至[!DNL Privacy Service]的身分都必須附有命名空間，該命名空間將身分值與其來源系統相關，以提供上下文。 命名空間可以代表一般概念，例如電子郵件地址（「電子郵件」），或將識別與特定應用程式(例如Adobe Advertising CloudID(「AdCloud」)或Adobe TargetID(「TNTID」))建立關聯。

Adobe Experience Platform身分服務會維護全域定義與使用者定義身分名稱空間的儲存。 有關名稱空間的詳細資訊，請參見[identity namespace overview](../identity-service/namespaces.md)。 有關[!DNL Privacy Service]中常用的標準名稱空間和名稱空間限定詞的清單，請參閱開發人員指南中的[附錄部分](api/appendix.md)。

## ECID與選擇加入服務

Adobe Experience Cloud[!DNL Identity Service]是[!DNL Experience Cloud]的通用識別架構，並為每個網站訪客指派唯一、永久的ID。 [!DNL Experience Cloud] ID(ECID)可透過使用第一方Cookie來追蹤客戶的活動，可以跨多個應用程式唯一識別裝置，並可讓您識別不同[!DNL Experience Cloud]應用程式中的相同網站訪客及其資料。 如需詳細資訊，請參閱[Experience Cloud身分服務概觀](https://docs.adobe.com/content/help/zh-Hant/id-service/using/intro/overview.html)。

選擇加入服務是[!DNL Experience Cloud Identity Service]的擴充功能，可讓您在應用程式上設定通訊協定，讓訪客決定您是否可在訪客的裝置或瀏覽器上設定Cookie。 有關選擇加入服務的詳細資訊，包括如何為您的應用程式設定服務，請參閱[選擇加入服務檔案](https://docs.adobe.com/content/help/zh-Hant/id-service/using/implementation/opt-in-service/optin-overview.html)。

一旦您的網站訪客獲得ECID，您就可以使用[!DNL Privacy JavaScript Library]Adobe來擷取這些ID，以用於隱私權要求，如下節所述。

## [!DNL Privacy JS Library]

[!DNL Adobe Privacy JavaScript Library]提供了幾個功能，允許您檢索和刪除儲存在瀏覽器中的客戶身份。 該庫可配置為從多個Adobe應用程式（包括ECID）檢索身份資訊。 透過使用回呼或承諾，您可以程式設計方式處理成功擷取的ID，並將它們傳送至[!DNL Privacy Service] API。

如需[!DNL Privacy JS Library]的詳細資訊，包括數個常用案例的程式碼範例，請參閱[隱私權JS程式庫概觀](js-library.md)。

## 後續步驟

本檔案簡要概述擷取客戶身分資料以用於隱私權要求的主要概念。 建議您檢閱各節中提供的檔案連結，以取得這些概念和服務的詳細資訊。 如需如何將擷取的ID傳送至[!DNL Privacy Service]以建立存取、刪除或選擇退出銷售要求的步驟，請參閱[Privacy Service開發人員指南](api/getting-started.md)。
