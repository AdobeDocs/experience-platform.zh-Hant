---
keywords: Experience Platform；主題；熱門主題；Marketo Engage；市場推廣；marketo engage;marketo
solution: Experience Platform
title: Marketo Engage連接器
description: 本文檔概述了Marketo Engage源連接器，包括有關其驗證、映射和資料延遲的資訊。
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: d8cd69524d984fdb828447287f3f4a4fe5913d61
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# [!DNL Marketo Engage] 連接器

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (以下簡稱：[!DNL Marketo]&quot;)是銷售線索管理和B2B營銷商的一個完整解決方案，希望通過參與複雜購買過程的每個階段來轉變客戶體驗。

使用 [!DNL Marketo] 源連接器，您可以從 [!DNL Marketo] 使用與平台連接的應用程式保持此資料的最新。

>[!IMPORTANT]
>
>您必須有權訪問 [Adobe Real-time Customer Data PlatformB2B版](../../../../rtcdp/b2b-overview.md) 使用所有Marketo資料集進行分割 [即時客戶配置檔案](../../../../profile/home.md)。 沒有Real-Time CDPB2B版，您仍然可以使用Marketo源將資料從人員和活動資料集帶到即時客戶概要檔案以進行細分。

此文檔概述 [!DNL Marketo] 源連接器，包括有關如何驗證連接器、如何映射的資訊 [!DNL Marketo] 以體驗資料模型(XDM)和連接器的資料延遲。

## 驗證您的 [!DNL Marketo] 連接器

為了連接 [!DNL Marketo] 到平台，必須首先檢索 `munchkinId`。 `clientId`, `clientSecret`。

請參閱 [驗證您的Marketo源連接器](./marketo-auth.md) 文檔以檢索您的憑據。

## 設定Adobe組織映射

在為 [!DNL Marketo]，必須首先設定Adobe組織映射。 有關如何完成此操作的詳細步驟，請參見上的指南 [設定Adobe組織映射 [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html)。

## 設定B2B命名空間和模式自動生成實用程式

接下來，使用B2B命名空間和模式自動生成實用程式來設定平台開發人員控制台和Postman環境。 這允許您自動填充B2B命名空間和架構。 有關詳細說明，請參閱上的指南 [設定B2B命名空間和模式自動生成實用程式](./marketo-namespaces.md)

## 體驗資料模型(XDM)

XDM是一個公開記錄的規範，它提供了通用的結構和定義，允許您從第三方源中接收資料以用於下游平台服務。

遵守XDM標準允許將資料統一地納入平台生態系統，使資料傳輸和資訊收集更加容易。

要瞭解有關XDM及其在平台中的角色的詳細資訊，請參閱 [XDM系統概述](../../../../xdm/home.md)。

## 欄位映射自 [!DNL Marketo] 到XDM

建立源連接 [!DNL Marketo] 而平台，在將Marketo源資料欄位納入平台之前，必須將其映射到相應的目標XDM欄位。

有關在以下位置之間的欄位映射規則的詳細資訊，請參閱以下 [!DNL Marketo] 資料集和平台：

* [活動](../mapping/marketo.md#activities)
* [方案](../mapping/marketo.md#programs)
* [程式成員資格](../mapping/marketo.md#program-memberships)
* [公司](../mapping/marketo.md#companies)
* [靜態清單](../mapping/marketo.md#static-lists)
* [靜態清單成員資格](../mapping/marketo.md#static-list-memberships)
* [命名帳戶](../mapping/marketo.md#named-accounts)
* [機會](../mapping/marketo.md#opportunities)
* [機會聯繫人角色](../mapping/marketo.md#opportunity-contact-roles)
* [人](../mapping/marketo.md#persons)

## 預期延遲 [!DNL Marketo] 平台上的資料

下表概述了預期的延遲 [!DNL Marketo] 根據接收的性質和期望的目標將資料導入平台：

| 目的地 | 預期延遲 |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt;1分鐘 |
| 達塔湖 | &lt; 60 分鐘 |

## 後續步驟和其他資源

以下文檔提供了有關建立 [!DNL Marketo] 源連接：

* 有關如何連接的資訊 [!DNL Marketo] 資料到平台，請閱讀上的教程 [建立 [!DNL Marketo] UI中的源連接](../../../tutorials/ui/create/adobe-applications/marketo.md)。
   * 有關如何設定架構和接收自定義活動資料的資訊，請閱讀上的教程 [建立源連接和資料流 [!DNL Marketo] 自定義活動資料](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
* 有關B2B命名空間和使用的架構的基礎設定的資訊 [!DNL Marketo]，閱讀文檔 [B2B命名空間和架構](./marketo-namespaces.md)。
* 有關查找 [!DNL Marketo] Munchkin ID和生成您的憑據，請閱讀 [[!DNL Marketo] 認證指南](./marketo-auth.md)。
* 有關適用於的特定映射規則的資訊 [!DNL Marketo] 資料集，閱讀文檔 [[!DNL Marketo] 欄位映射](../mapping/marketo.md)。
* 有關 [!DNL Real-Time Customer Data Platform B2B Edition] 及其功能，閱讀 [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md)。
