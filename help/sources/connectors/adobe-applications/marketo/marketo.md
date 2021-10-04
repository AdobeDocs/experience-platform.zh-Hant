---
keywords: Experience Platform；首頁；熱門主題；Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: Marketo Engage連接器
topic-legacy: overview
description: 本檔案概述Marketo Engage來源連接器，包括驗證、對應和資料延遲的相關資訊。
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 0661d124ffe520697a1fc8e2cae7b0b61ef4edfc
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# (Beta)[!DNL Marketo Engage]連接器

>[!IMPORTANT]
>
>Adobe Experience Platform中的[!DNL Marketo Engage]來源目前為測試版。 檔案和功能可能會有所變更。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (以下稱為「[!DNL Marketo]」)是銷售機會管理的完整解決方案，適合B2B行銷人員使用，而透過該解決方案，他們可參與複雜購買歷程的每個階段，從中轉變客戶體驗。

使用[!DNL Marketo]源連接器，可以將[!DNL Marketo]的B2B資料帶入Platform，並使用與平台連接的應用程式保持此資料的最新。

本檔案概述[!DNL Marketo]來源連接器，包括如何驗證連接器、如何將[!DNL Marketo]欄位對應至Experience Data Model(XDM)，以及連接器的資料延遲的相關資訊。

## 驗證[!DNL Marketo]連接器

若要將[!DNL Marketo]連線至Platform，您必須先擷取`munchkinId`、`clientId`和`clientSecret`的值。

請參閱[驗證Marketo來源連接器](./marketo-auth.md)檔案中概述的步驟，以擷取您的憑證。

## Experience Data Model(XDM)

XDM是公開記錄的規格，提供通用結構和定義，可讓您內嵌來自協力廠商來源的資料，以用於下游Platform服務。

遵循XDM標準，即可將資料統一整合至Platform生態系統，更輕鬆傳送資料和收集資訊。

若要進一步了解XDM及其在Platform中的角色，請參閱[XDM系統概述](../../../../xdm/home.md)。

## 從[!DNL Marketo]到XDM的欄位映射

若要在[!DNL Marketo]和Platform之間建立來源連線，Marketo來源資料欄位在匯入至Platform之前，必須先對應至其適當的目標XDM欄位。

如需[!DNL Marketo]資料集和Platform之間欄位對應規則的詳細資訊，請參閱下列內容：

* [活動](../mapping/marketo.md#activities)
* [計劃](../mapping/marketo.md#programs)
* [方案成員資格](../mapping/marketo.md#program-memberships)
* [公司](../mapping/marketo.md#companies)
* [靜態清單](../mapping/marketo.md#static-lists)
* [靜態清單成員資格](../mapping/marketo.md#static-list-memberships)
* [已命名帳戶](../mapping/marketo.md#named-accounts)
* [機會](../mapping/marketo.md#opportunities)
* [機會聯繫人角色](../mapping/marketo.md#opportunity-contact-roles)
* [人員](../mapping/marketo.md#persons)

## 平台上[!DNL Marketo]資料的預期延遲

下表根據擷取的性質和所需目的地，概述將[!DNL Marketo]資料匯入Platform的預期延遲：

| 目的地 | 預期延遲 |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| 資料湖 | &lt; 60 分鐘 |

## 後續步驟和其他資源

以下文檔提供了有關建立[!DNL Marketo]源連接的詳細資訊：

* 如需如何將[!DNL Marketo]資料連線至Platform的詳細資訊，請參閱UI](../../../tutorials/ui/create/adobe-applications/marketo.md)中[建立Marketo來源連接器的教學課程。
* 有關[!DNL Marketo]使用的B2B命名空間和結構的基礎設定的資訊，請參閱[B2B命名空間和結構](./marketo-namespaces.md)的文檔。
* 有關查找[!DNL Marketo]用戶ID和生成憑據的資訊，請參閱[[!DNL Marketo] authentication guide](./marketo-auth.md)。
* 有關適用於[!DNL Marketo]資料集的特定映射規則的資訊，請參閱[[!DNL Marketo] 欄位映射](../mapping/marketo.md)的相關檔案。
* 有關[!DNL Real-time Customer Data Platform B2B Edition]及其功能的一般資訊，請參閱[[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md)上的文檔。
