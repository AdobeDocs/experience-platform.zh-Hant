---
keywords: 標識rtcdp;rtcdp標識；即時cdp標識
title: Real-time Customer Data Platform身份
description: Adobe Experience Platform身份服務通過跨設備和系統將身份連接在一起，幫助您更好地瞭解客戶及其行為。
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# 身份概述

Adobe Experience Platform [!DNL Identity Service] 通過跨設備和系統將身份連接在一起，幫助您更好地瞭解客戶及其行為。 通常，您的客戶會通過多個渠道與您的品牌進行互動，這可能包括線上瀏覽您的網站、在店內購買、加入您的忠誠計畫或致電幫助台尋求支援等。 在這些多個系統中，為該客戶建立了一個標識， [!DNL Identity Service] 使這些身份能夠一起看完整的圖片。

現在，您可以看到，與您的品牌在五個不同渠道進行互動的不是五個不同的客戶，而是同一個客戶，而且您可以確保他們通過每次互動獲得一致、個性化且相關的體驗。 隨著有關客戶的更多資訊（例如，您的網站的匿名瀏覽器決定註冊帳戶並登錄）逐漸被縫合，客戶的圖片變得越來越清晰。

## 身分識別命名空間

標識命名空間是 [!DNL Identity Service] 並作為指標，為客戶身份提供附加的上下文。 一個常用ID命名空間的示例是「電子郵件」，其中跨多個網站使用相同的電子郵件地址允許您將多個不同的身份組合在一起，每個身份都具有一個唯一的客戶ID，實際上屬於同一個客戶。 [!DNL Experience Platform] 允許您使用ID命名空間在用戶介面中搜索各個配置檔案。 有關查看配置檔案的詳細資訊，請參閱 [配置檔案瀏覽概述](profile-browse.md)。 要瞭解有關標識命名空間的詳細資訊，請參見 [標識命名空間概述](../../identity-service/namespaces.md)。

## 標識圖

標識圖是不同標識名稱空間之間關係的映射，它為您提供了客戶如何通過不同渠道與您的品牌交互的直觀表示。 所有客戶標識圖由 [!DNL Identity Service] 響應客戶活動。

[!DNL Identity Service] 管理僅由您的組織可見並基於您的資料構建的標識圖（稱為專用圖）。 [!DNL Identity Service] 當所接收的資料記錄包含多個身份時，將擴展您的私有圖形，並在找到的身份之間添加關係。

## 後續步驟

身份及其之間的關係由 [!DNL Identity Service] 和 [!DNL Real-Time Customer Profile] 全面瞭解每個客戶及其交互過程。 要瞭解更多資訊，請訪問 [Identity Service文檔](../../identity-service/home.md)。
