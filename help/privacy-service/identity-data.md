---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 隱私權要求的身分資料
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 3%

---


# 隱私權要求的身分資料

為了讓Adobe Experience Platform處理客戶對其私人資料（包括存取、刪除或選擇退出銷售要求）的要求，必須提供唯一識別碼，將特定客戶連結至您啟用Adobe Experience Cloud的應用程式中儲存的私人資料。 [!DNL Privacy Service] [!DNL Privacy Service] 然後使用這些識別碼來收集客戶識別碼下儲存的所有資料 [!DNL Experience Cloud]，並根據客戶的要求加以處理。

本檔案提供如何設定資料作業的一般指引，並運用Adobe技術，以有效擷取適當的客戶隱私權要求識別資訊。

## 身分與名稱空間

當客戶可以透過數個不同通道與您的品牌互動時，要協調從這些眾多互動中記錄的不同識別碼可能非常困難。 這反過來又會讓您難以判斷哪些資料屬於您應用程式中的特定人 [!DNL Experience Cloud] 員。

例如，在中處理客戶資料請求時 [!DNL Privacy Service]，身分可代表在Adobe控制網域下設定的Cookie值、在協力廠商網域下並與Adobe共用的Cookie值，或您在IMS組織內明確定義的自訂識別碼。

因此，每個傳送到的身分都必須 [!DNL Privacy Service] 附帶命名空間 **** ，該名稱空間將身分值與其來源系統關聯，以提供上下文。 命名空間可以代表一般概念，例如電子郵件地址（「電子郵件」），或將身分識別與特定應用程式(例如Adobe Advertising Cloud ID(「AdCloud」)或Adobe Target ID(「TNTID」))建立關聯。

Adobe Experience Platform Identity Service會維護全域定義與使用者定義之識別名稱空間的存放區。 如需名稱空間的詳細資訊，請參閱 [身分名稱空間概觀](../identity-service/namespaces.md)。 如需常用於的標準名稱空間和名稱空間限定詞的清單 [!DNL Privacy Service]，請參閱開發 [人員指南的附](api/appendix.md) 錄。

## ECID與選擇加入服務

Adobe Experience Cloud可 [!DNL Identity Service] 做為每個網站訪客的通用識別 [!DNL Experience Cloud]架構，並為每個網站訪客指派唯一、永久的ID。 ID( [!DNL Experience Cloud] ECID)可透過使用第一方Cookie來追蹤客戶的活動，可以跨多個應用程式唯一識別裝置，並可讓您識別不同應用程式中的相同網站訪客及其資 [!DNL Experience Cloud] 料。 See the [Experience Cloud Identity Service overview](https://docs.adobe.com/content/help/zh-Hant/id-service/using/intro/overview.html) for more information.

「選擇加入服務」是應用程式的延 [!DNL Experience Cloud Identity Service]伸功能，可讓您在應用程式上設定通訊協定，讓訪客決定您是否可在訪客的裝置或瀏覽器上設定Cookie。 如需有關選擇加入服務的詳細資訊，包括如何為您的應用程式設定服務，請參閱選擇 [加入服務檔案](https://docs.adobe.com/content/help/zh-Hant/id-service/using/implementation/opt-in-service/optin-overview.html)。

一旦您的網站訪客獲得ECID，您就可以利用Adobe [!DNL Privacy JavaScript Library] 擷取這些ID，以便用於隱私權要求，如下節所述。

## [!DNL Privacy JS Library]

它提 [!DNL Adobe Privacy JavaScript Library] 供幾種功能，可讓您擷取和移除儲存在瀏覽器中的客戶身分識別。 程式庫可設定為從數個Adobe應用程式（包括ECID）擷取身分資訊。 透過使用回呼或承諾，您可以程式設計方式處理成功擷取的ID，並將它們傳送至 [!DNL Privacy Service] API。

如需詳細資訊 [!DNL Privacy JS Library]，包括數種常見使用案例的程式碼範例，請參閱「隱私 [權JS程式庫」概觀](js-library.md)。

## 後續步驟

本檔案簡要概述擷取客戶身分資料以用於隱私權要求的主要概念。 建議您檢閱各節中提供的檔案連結，以取得這些概念和服務的詳細資訊。 如需如何傳送擷取的ID [!DNL Privacy Service] 至建立存取、刪除或選擇退出銷售要求的步驟，請參閱隱私服務開 [發人員指南](api/getting-started.md)。