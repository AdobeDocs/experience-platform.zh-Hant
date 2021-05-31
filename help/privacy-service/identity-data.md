---
keywords: Experience Platform；首頁；熱門主題；ECID;ecid
solution: Experience Platform
title: 隱私權要求的身分資料
topic-legacy: overview
description: 本檔案提供如何設定資料操作及運用Adobe技術，以有效擷取適當客戶隱私權要求身分資訊的一般指引。
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: d316c199c7e2d87d175015c1828af6fd0d57f32a
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 1%

---

# 隱私權要求的身分資料

為了讓Adobe Experience Platform [!DNL Privacy Service]處理客戶對其私人資料（包括存取、刪除或選擇退出銷售請求）的請求，必須提供唯一識別碼，將特定客戶連結至其在您啟用Adobe Experience Cloud的應用程式中儲存的私人資料。 [!DNL Privacy Service] 然後使用這些識別碼來收集內儲存在客戶身分識別下的所有 [!DNL Experience Cloud]資料，並根據客戶的要求加以處理。

本檔案提供如何設定資料操作及運用Adobe技術，以有效擷取適當客戶隱私權要求身分資訊的一般指引。

## 身分識別與命名空間

當客戶可透過數個不同管道與您的品牌互動時，若要協調從這些多次互動中記錄的不同識別碼，可能會很困難。 這反過來又會使您難以判斷哪些資料屬於[!DNL Experience Cloud]應用程式中的特定人員。

例如，在[!DNL Privacy Service]中處理客戶資料請求時，身分可代表在Adobe控制網域下設定的Cookie值、在協力廠商網域下並與Adobe共用的Cookie值，或您在IMS組織中明確定義的自訂識別碼。

因此，傳送至[!DNL Privacy Service]的每個身分都須搭配命名空間，以提供內容，方法是將身分值與其來源系統相關。 命名空間可代表一般概念，例如電子郵件地址（「電子郵件」），或將身分識別與特定應用程式建立關聯，例如Adobe Advertising Cloud ID(「AdCloud」)或Adobe Target ID(「TNTID」)。

Adobe Experience Platform Identity Service會維護全域定義及使用者定義身分識別命名空間的存放區。 如需命名空間的詳細資訊，請參閱[身分命名空間概述](../identity-service/namespaces.md)。 有關[!DNL Privacy Service]中常用的標準命名空間和命名空間限定符的清單，請參閱開發人員指南中的[附錄部分](api/appendix.md)。

## ECID與選擇加入服務

Adobe Experience Cloud [!DNL Identity Service]可作為[!DNL Experience Cloud]的共同識別架構，並為每個網站訪客指派不重複的永久ID。 [!DNL Experience Cloud] ID(ECID)可透過使用第一方Cookie來追蹤客戶的活動，並可跨多個應用程式唯一識別裝置，且可讓您在不同的[!DNL Experience Cloud]應用程式中識別相同的網站訪客及其資料。 如需詳細資訊，請參閱[Experience Cloud身分服務概述](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) 。

選擇加入服務是[!DNL Experience Cloud Identity Service]的擴充功能，可讓您在應用程式上設定通訊協定，讓訪客決定您是否可以在訪客的裝置或瀏覽器上設定Cookie。 如需選擇加入服務的詳細資訊，包括如何設定您應用程式的服務，請參閱[選擇加入服務檔案](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=zh-Hant)。

為您的網站訪客指派ECID後，您就可以利用[!DNL Privacy JavaScript Library]Adobe，擷取這些ID以用於隱私權請求，如下一節所述。

## [!DNL Privacy JS Library]

[!DNL Adobe Privacy JavaScript Library]提供數個功能，可讓您擷取和移除儲存在瀏覽器中的客戶身分識別。 程式庫可設定為從數個Adobe應用程式（包括ECID）擷取身分資訊。 透過使用回呼或承諾，您可以以程式設計方式處理成功擷取的ID，並將其傳送至[!DNL Privacy Service] API。

如需[!DNL Privacy JS Library]的詳細資訊，包括數種常見使用案例的程式碼範例，請參閱[隱私權JS程式庫概觀](js-library.md)。

## 後續步驟

本檔案簡要概述擷取客戶身分資料以用於隱私權要求的核心概念。 建議您檢閱每個區段中提供的檔案連結，以取得這些概念和服務的詳細資訊。 如需如何將擷取的ID傳送至[!DNL Privacy Service]以建立存取、刪除或選擇退出銷售請求的步驟，請參閱[Privacy Service開發人員指南](api/getting-started.md)。
