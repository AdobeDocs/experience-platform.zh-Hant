---
keywords: Experience Platform；首頁；熱門主題；ECID；ecid
solution: Experience Platform
title: 隱私權請求的身分資料
description: 本檔案提供的一般指引，說明如何設定資料作業，並運用Adobe技術有效擷取適合客戶隱私權請求的身分資訊。
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---

# 隱私權要求的身分識別資料

為了讓Adobe Experience Platform [!DNL Privacy Service]處理客戶對其私人資料的請求（包括存取、刪除或選擇退出銷售請求），必須提供唯一識別碼，將特定客戶與其在啟用Adobe Experience Cloud的應用程式中儲存的私人資料連結。 [!DNL Privacy Service]接著會使用這些識別碼來收集儲存在[!DNL Experience Cloud]內客戶身分下的所有資料，並根據客戶的請求加以處理。

本檔案提供的一般指引，說明如何設定資料作業，並運用Adobe技術有效擷取適合客戶隱私權請求的身分資訊。

## 身分和名稱空間

當客戶可以透過數個不同的管道與您的品牌互動時，要協調從這些許多互動中記錄的不同識別碼會很困難。 這進而會使得難以判斷哪些資料屬於您[!DNL Experience Cloud]應用程式中的特定人員。

例如，在[!DNL Privacy Service]中處理客戶資料請求時，身分識別可能代表在Adobe控制的網域下設定的Cookie值、在第三方網域下並與Adobe共用的Cookie值，或您在組織內明確定義的自訂識別碼。

因此，每個傳送至[!DNL Privacy Service]的身分都必須隨附名稱空間，該名稱空間會將身分值關聯至其來源系統，以提供內容。 名稱空間可代表一般概念，例如電子郵件地址（「電子郵件」），或將身分與特定應用程式相關聯，例如Adobe Advertising Cloud ID (「AdCloud」)或Adobe Target ID (「TNTID」)。

Adobe Experience Platform Identity Service維護全域定義和使用者定義的身分名稱空間儲存。 如需名稱空間的詳細資訊，請參閱[身分名稱空間概觀](../identity-service/features/namespaces.md)。 如需[!DNL Privacy Service]中常用的標準名稱空間和名稱空間限定詞清單，請參閱API指南中的[附錄區段](api/appendix.md)。

## ECID和選擇加入服務

Adobe Experience Cloud [!DNL Identity Service]可作為[!DNL Experience Cloud]的共同識別架構，並為每個網站訪客指派不重複的永久ID。 [!DNL Experience Cloud] ID (ECID)透過使用第一方Cookie來追蹤客戶活動，可唯一識別多個應用程式中的裝置，並可讓您識別不同[!DNL Experience Cloud]應用程式中的相同網站訪客及其資料。 如需詳細資訊，請參閱[Experience Cloud識別服務總覽](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant)。

選擇加入服務是[!DNL Experience Cloud Identity Service]的擴充功能，可讓您在應用程式上設定通訊協定，讓訪客判斷您是否可以在訪客的裝置或瀏覽器上設定Cookie。 如需選擇加入服務的詳細資訊，包括如何設定應用程式的服務，請參閱[選擇加入服務檔案](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html)。

為您的網站訪客指派ECID後，您就可以利用Adobe[!DNL Privacy JavaScript Library]來擷取這些ID，以用於隱私權要求，如下節所述。

## [!DNL Privacy JS Library]

[!DNL Adobe Privacy JavaScript Library]提供數個功能，可讓您擷取及移除儲存在瀏覽器中的客戶身分識別。 程式庫可設定為從數個Adobe應用程式（包括ECID）擷取身分資訊。 透過使用回呼或承諾，您可以程式設計方式處理成功擷取的ID，並將其傳送至[!DNL Privacy Service] API。

如需[!DNL Privacy JS Library]的詳細資訊，包括幾個常見使用案例的程式碼範例，請參閱[隱私權JS程式庫概觀](js-library.md)。

## 後續步驟

本檔案簡要概述擷取客戶身分資料以用於隱私權請求時的主要概念。 建議您檢閱每個區段提供的檔案連結，以取得這些概念與服務的詳細資訊。 如需如何將擷取的ID傳送至[!DNL Privacy Service]以建立存取、刪除或選擇退出銷售請求的步驟，請參閱[Privacy ServiceAPI指南](api/overview.md)。
