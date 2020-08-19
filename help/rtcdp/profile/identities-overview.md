---
keywords: identities rtcdp;rtcdp identities;real-time cdp identities
title: 即時CDP中的身份
description: Adobe Experience Platform Identity Service可跨裝置和系統將身分連結在一起，協助您更全面地瞭解客戶及其行為。
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# 即時CDP中的身份

Adobe Experience Platform可協 [!DNL Identity Service] 助您跨裝置和系統將身分連接在一起，以更全面地瞭解客戶及其行為。 通常，您的客戶會透過多個通道與您的品牌互動，其中可能包括線上瀏覽您的網站、在店內購買、加入您的忠誠度計畫，或致電服務台尋求支援等。 在這些多個系統中，會為該客戶建立一個識別碼， [!DNL Identity Service] 讓這些識別碼能夠整合在一起，以檢視完整圖景。

現在，您可以看到，這是同一個客戶，而不是透過五個不同的通道與您的品牌互動的5個不同客戶，而且您可以確保他們透過每次互動獲得一致、個人化、相關的體驗。 隨著更多有關客戶的資訊（例如，您網站的匿名瀏覽器決定註冊帳戶和登入），這些資訊會被銜接在一起，而客戶的形象也變得越來越清晰。

## 身分名稱空間

身份名稱空間是客戶身 [!DNL Identity Service] 份的一個元件，並作為提供客戶身份的附加上下文的指標。 常用ID命名空間的範例是「電子郵件」，在多個網站上使用相同的電子郵件地址可讓您將多個不同的身分識別接合在一起，每個身分識別碼都具有唯一的客戶ID，實際上屬於同一客戶。 [!DNL Experience Platform] 可讓您使用ID名稱空間在使用者介面中搜尋個別描述檔。 如需檢視描述檔的詳細資訊，請參閱描述檔檢 [視器概觀](/help/rtcdp/profile/profile-viewer.md)。 若要進一步瞭解身分名稱空間，請參閱 [身分名稱空間概觀](../../identity-service/namespaces.md)。

## 身分圖

身分圖是不同身分名稱空間之間關係的地圖，提供您視覺化的呈現方式，說明客戶如何透過不同通道與您的品牌互動。 所有客戶識別圖表都會以近乎即時的 [!DNL Identity Service] 方式共同管理和更新，以回應客戶活動。

[!DNL Identity Service] 管理僅由您的組織可見的識別圖形，並根據您的資料（稱為專用圖形）建立。 [!DNL Identity Service] 當收錄的資料記錄包含多個身分時，增加您的私人圖表，並在找到的身分之間新增關係。

## 後續步驟

身分及其間的關係，都由定義和維護， [!DNL Identity Service] 並運用來 [!DNL Real-time Customer Profile] 建立每位個別客戶及其互動的完整圖景。 若要進一步瞭解，請造訪 [Identity Service檔案](../../identity-service/home.md)。