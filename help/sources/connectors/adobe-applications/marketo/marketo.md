---
keywords: Experience Platform；首頁；熱門主題；Marketo Engage；行銷人員；行銷人員
solution: Experience Platform
title: Marketo Engage連接器
topic: 概述
description: 本檔案概述Marketo Engage來源連接器，包括驗證、對應和資料延遲的相關資訊。
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---


# （測試版）[!DNL Marketo Engage]連接器

>[!IMPORTANT]
>
>[!DNL Marketo Engage]來源目前處於測試階段。 其功能和說明檔案可能會有所變更。

Adobe Experience Platform允許從外部來源接收資料，同時提供使用平台服務構建、標籤和增強傳入資料的能力。 您可以從多種來源收錄資料，例如Adobe應用程式、雲端儲存空間、資料庫等。

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (以下稱為「[!DNL Marketo]」)是銷售機會管理和B2B行銷人員的完整解決方案，希望透過參與複雜購買歷程的每個階段來轉變客戶體驗。

使用[!DNL Marketo]源連接器，可以將[!DNL Marketo]的B2B資料帶入平台，並使用與平台連接的應用程式保持此資料的最新狀態。

本檔案概述[!DNL Marketo]來源連接器，包括如何驗證連接器、如何將[!DNL Marketo]欄位對應至Experience Data Model(XDM)，以及連接器的資料延遲。

## 驗證[!DNL Marketo]連接器

為了將[!DNL Marketo]連接到平台，您必須首先檢索`munchkinId`、`clientId`和`clientSecret`的值。

請參閱[驗證您的Marketo源連接器](./marketo-auth.md)文檔中概述的步驟以檢索您的憑據。

## 體驗資料模型(XDM)

XDM是公開記載的規格，可提供常用的結構和定義，讓您從協力廠商來源擷取資料，以便用於下游平台服務。

遵循XDM標準可讓資料統一地整合到平台生態系統中，讓資料傳遞和收集資訊變得更輕鬆。

要瞭解有關XDM及其在平台中的角色的更多資訊，請參見[XDM系統概述](../../../../xdm/home.md)。

## 從[!DNL Marketo]到XDM的欄位映射

要在[!DNL Marketo]和平台之間建立源連接，Marketo源資料欄位必須映射到其適當的目標XDM欄位，才能被引入平台。

有關[!DNL Marketo]資料集和平台之間的欄位映射規則的詳細資訊，請參見以下內容：

* [活動](../mapping/marketo.md#activities)
* [計劃](../mapping/marketo.md#programs)
* [方案會籍](../mapping/marketo.md#program-memberships)
* [公司](../mapping/marketo.md#companies)
* [靜態清單](../mapping/marketo.md#static-lists)
* [靜態清單成員資格](../mapping/marketo.md#static-list-memberships)
* [命名帳戶](../mapping/marketo.md#named-accounts)
* [機會](../mapping/marketo.md#opportunities)
* [業務機會聯繫人角色](../mapping/marketo.md#opportunity-contact-roles)
* [人物](../mapping/marketo.md#persons)

## 平台上[!DNL Marketo]資料的預期延遲

下表概述根據擷取的性質和所需目的地，將[!DNL Marketo]資料匯入平台的預期延遲：

| 目的地 | 預期延遲 |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60 分鐘 |

## 後續步驟和其他資源

以下文檔提供了有關建立[!DNL Marketo]源連接的詳細資訊：

* 有關如何將[!DNL Marketo]資料連接到平台的資訊，請參閱UI](../../../tutorials/ui/create/adobe-applications/marketo.md)中有關建立Marketo源連接器的教程。[
* 有關[!DNL Marketo]使用的B2B名稱空間和架構的基礎設定的資訊，請參見[B2B名稱空間和架構](./marketo-namespaces.md)的文檔。
* 有關查找[!DNL Marketo] munchkin ID和生成憑據的資訊，請參閱[[!DNL Marketo] 身份驗證指南](./marketo-auth.md)。
* 有關適用於[!DNL Marketo]資料集的特定映射規則的資訊，請參見[[!DNL Marketo] 欄位映射](../mapping/marketo.md)上的文檔。