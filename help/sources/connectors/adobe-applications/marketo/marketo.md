---
keywords: Experience Platform；首頁；熱門主題；Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: Marketo Engage連接器
description: 本檔案概述Marketo Engage來源連接器，包括驗證、對應和資料延遲的相關資訊。
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: d8cd69524d984fdb828447287f3f4a4fe5913d61
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# [!DNL Marketo Engage] 連接器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (下稱「[!DNL Marketo]「)是銷售機會管理的完整解決方案，適合B2B行銷人員使用，而透過該解決方案，他們可參與複雜購買歷程的每個階段，從中轉變客戶體驗。

使用 [!DNL Marketo] 來源連接器，您可以將B2B資料 [!DNL Marketo] 使用與平台連線的應用程式，讓此資料保持最新。

>[!IMPORTANT]
>
>您必須擁有 [Adobe Real-time Customer Data Platform B2B版](../../../../rtcdp/b2b-overview.md) 若要使用所有Marketo資料集來劃分 [即時客戶個人檔案](../../../../profile/home.md). 若沒有Real-Time CDP B2B Edition，您仍可以使用Marketo來源，將人員和活動資料集的資料匯入即時客戶設定檔，以便進行細分。

本檔案概述 [!DNL Marketo] 源連接器，包括如何驗證連接器、如何映射 [!DNL Marketo] 欄位至Experience Data Model(XDM)，以及連接器的資料延遲。

## 驗證您的 [!DNL Marketo] 連接器

為了連接 [!DNL Marketo] 若為Platform，您必須先擷取 `munchkinId`, `clientId`，和 `clientSecret`.

請參閱 [驗證您的Marketo來源連接器](./marketo-auth.md) 文檔以檢索您的憑據。

## 設定Adobe組織對應

建立映射集之前 [!DNL Marketo]，您必須先設定Adobe組織對應。 如需如何完成此作業的詳細步驟，請參閱 [設定Adobe組織映射 [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## 設定B2B命名空間和架構自動產生公用程式

接下來，使用B2B命名空間和結構自動產生公用程式來設定您的平台開發人員主控台和Postman環境。 這可讓您自動填入B2B命名空間和結構。 如需詳細指示，請參閱 [設定B2B命名空間和架構自動產生公用程式](./marketo-namespaces.md)

## Experience Data Model(XDM)

XDM是公開記錄的規格，提供通用結構和定義，可讓您內嵌來自協力廠商來源的資料，以用於下游Platform服務。

遵循XDM標準，即可將資料統一整合至Platform生態系統，更輕鬆傳送資料和收集資訊。

若要進一步了解XDM及其在Platform中的角色，請參閱 [XDM系統概觀](../../../../xdm/home.md).

## 欄位對應來源 [!DNL Marketo] 到XDM

在 [!DNL Marketo] 和Platform,Marketo來源資料欄位必須先對應至其適當的目標XDM欄位，才能匯入Platform。

請參閱下列內容，以取得關於 [!DNL Marketo] 資料集和Platform:

* [活動](../mapping/marketo.md#activities)
* [計畫](../mapping/marketo.md#programs)
* [方案成員資格](../mapping/marketo.md#program-memberships)
* [公司](../mapping/marketo.md#companies)
* [靜態清單](../mapping/marketo.md#static-lists)
* [靜態清單成員資格](../mapping/marketo.md#static-list-memberships)
* [已命名帳戶](../mapping/marketo.md#named-accounts)
* [機會](../mapping/marketo.md#opportunities)
* [機會聯繫人角色](../mapping/marketo.md#opportunity-contact-roles)
* [人員](../mapping/marketo.md#persons)

## 預期延遲 [!DNL Marketo] Platform上的資料

下表概述將 [!DNL Marketo] 根據擷取的性質和所需目的地，將資料匯入Platform:

| 目的地 | 預期延遲 |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 1分鐘 |
| 資料湖 | &lt; 60 分鐘 |

## 後續步驟和其他資源

下列檔案提供建立 [!DNL Marketo] 源連接：

* 有關如何連接您的 [!DNL Marketo] 資料至Platform，請閱讀以下教學課程： [建立 [!DNL Marketo] UI中的源連接](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * 如需如何設定結構以及擷取自訂活動資料的詳細資訊，請參閱的教學課程 [建立源連接和資料流 [!DNL Marketo] 自訂活動資料](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
* 如需B2B命名空間和結構的基礎設定相關資訊，請參閱 [!DNL Marketo]，請閱讀 [B2B命名空間和結構](./marketo-namespaces.md).
* 如需尋找 [!DNL Marketo] munchkin ID和產生憑證，請參閱 [[!DNL Marketo] 驗證指南](./marketo-auth.md).
* 有關適用於的特定映射規則的資訊 [!DNL Marketo] 資料集，請閱讀 [[!DNL Marketo] 欄位對應](../mapping/marketo.md).
* 有關 [!DNL Real-Time Customer Data Platform B2B Edition] 及其功能，請參閱 [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
