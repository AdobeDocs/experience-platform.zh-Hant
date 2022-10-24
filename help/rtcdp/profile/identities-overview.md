---
keywords: 身分識別rtcdp;rtcdp身分識別；即時cdp身分識別
title: Real-time Customer Data Platform身分
description: Adobe Experience Platform Identity Service可協助您跨裝置和系統橋接身分，以更全面了解客戶及其行為。
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# 身分概述

Adobe Experience Platform [!DNL Identity Service] 可協助您跨裝置和系統橋接身分，以更全面了解客戶及其行為。 通常，您的客戶會透過多個管道與您的品牌互動，包括線上瀏覽您的網站、在店內購買、加入您的忠誠計畫，或致電支援服務台等。 在這多個系統中，會為該客戶建立身分識別， [!DNL Identity Service] 使這些身份能夠一起呈現完整圖景。

現在，與其說五個不同的客戶跨五個不同管道與您的品牌互動，您可以看到這是同一個客戶，而且您可以確保他們透過每次互動獲得一致、個人化且相關的體驗。 隨著有關客戶的更多資訊（例如，您網站的匿名瀏覽器決定註冊帳戶並登入），該資訊便會匯整在一起，而客戶的形象也越來越清晰。

## 身分識別命名空間

身分識別命名空間是 [!DNL Identity Service] 並可作為指標，為客戶身分提供額外內容。 常用ID命名空間的範例是「電子郵件」，在多個網站上使用相同的電子郵件地址，可讓您拼接多個不同的身分資料，每個身分資料都有一個唯一的客戶ID，實際上屬於同一個客戶。 [!DNL Experience Platform] 可讓您使用ID命名空間來搜尋使用者介面中的個別設定檔。 如需檢視設定檔的詳細資訊，請參閱 [設定檔瀏覽概觀](profile-browse.md). 若要進一步了解身分識別命名空間，請參閱 [身分命名空間概述](../../identity-service/namespaces.md).

## 身分圖

身分圖表是不同身分識別命名空間之間關係的對應圖，可以以視覺化呈現客戶如何透過不同管道與品牌互動。 所有客戶身分圖表由共同管理和更新 [!DNL Identity Service] 以回應客戶活動。

[!DNL Identity Service] 管理僅由您的組織可見且根據您的資料（稱為專用圖表）建立的身分圖表。 [!DNL Identity Service] 擷取的資料記錄包含多個身分，並在找到的身分之間新增關係時，可擴大您的私人圖表。

## 後續步驟

身分及其間的關係由 [!DNL Identity Service] 和 [!DNL Real-time Customer Profile] 以建立每個個別客戶及其互動的完整畫面。 若要進一步了解，請造訪 [Identity服務檔案](../../identity-service/home.md).
