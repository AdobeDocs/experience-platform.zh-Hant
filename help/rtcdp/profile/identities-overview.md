---
keywords: 身分rtcdp；rtcdp身分；real-time cdp身分
title: Real-time Customer Data Platform中的身分
description: Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，協助您更清楚瞭解客戶及其行為。
feature: Get Started, Identities
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# 身分概述

Adobe Experience Platform [!DNL Identity Service]可協助您跨裝置和系統橋接身分，以更清楚瞭解客戶及其行為。 通常您的客戶會透過多個管道與您的品牌互動，可能包括線上瀏覽您的網站、在店內購買、加入您的忠誠度計畫或致電服務檯尋求支援，等等。 在這多個系統中，會為該客戶建立身分識別，[!DNL Identity Service]可讓這些身分識別整合在一起，以檢視完整畫面。

現在，不再是五個不同的客戶在五個不同的管道與您的品牌互動，您可以看到這是同一個客戶，並且您可以確保他們透過每次互動獲得一致、個人化的相關體驗。 隨著更多關於您客戶的資訊逐漸為人所知（例如，您網站的匿名瀏覽器決定註冊一個帳戶並登入），該資訊將會拼接在一起，而您客戶的圖片會變得越來越清晰。

## 身分識別命名空間

身分識別名稱空間是[!DNL Identity Service]的元件，可作為指標，為客戶身分識別提供額外的內容。 「電子郵件」是常用ID名稱空間的範例，在此範例中，跨多個網站使用相同的電子郵件地址，可讓您彙整多個不同的身分識別，每個識別都有一個唯一的客戶ID，而且實際上屬於同一個客戶。 [!DNL Experience Platform]可讓您使用ID名稱空間在使用者介面中搜尋個別設定檔。 如需檢視設定檔的詳細資訊，請參閱[設定檔瀏覽概觀](profile-browse.md)。 若要深入瞭解身分識別名稱空間，請參閱[身分識別名稱空間概觀](../../identity-service/features/namespaces.md)。

## 身分圖

身分圖表是不同身分之間的關係圖，可讓您以視覺化方式呈現客戶如何跨不同管道與您的品牌互動。 所有客戶身分圖表會由Identity Service集體管理及更新，以回應客戶活動。

[!DNL Identity Service]管理僅對您的組織可見且以您的資料為基礎的身分圖表。 當擷取的資料記錄包含多個身分時，[!DNL Identity Service]會增加您的圖表，在找到的身分之間新增關係。

## 後續步驟

身分以及他們之間的關係，是由[!DNL Identity Service]定義及維護，並由[!DNL Real-Time Customer Profile]運用，以建立每個個別客戶及其互動的完整面貌。 若要深入瞭解，請瀏覽[Identity Service檔案](../../identity-service/home.md)。
