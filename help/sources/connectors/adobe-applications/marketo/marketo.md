---
keywords: Experience Platform；首頁；熱門主題；Marketo Engage；marketo engage；marketo
solution: Experience Platform
title: Marketo Engage聯結器
description: 本檔案提供Marketo Engage來源聯結器的概觀，包括其驗證、對應和資料延遲的相關資訊。
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 50b97ebb8496636a0fccd64d57d7829b1342f87c
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 5%

---

# [!DNL Marketo Engage] 聯結器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

[[!DNL Marketo Engage]](https://www.marketo.com/software/) 是銷售機會管理的完整解決方案，也適合 B2B 行銷人員使用，而透過該解決方案，他們可參與複雜購買歷程的每個階段，從中轉變客戶體驗。

使用 [!DNL Marketo Engage] 來源聯結器，您可從以下來源取得B2B資料： [!DNL Marketo Engage] 至平台，並使用平台連線的應用程式保持這些資料在最新狀態。

>[!IMPORTANT]
>
>您必須有權存取 [Adobe Real-time Customer Data Platform B2B版本](../../../../rtcdp/b2b-overview.md) 若要使用所有Marketo資料集進行分段，請依 [即時客戶個人檔案](../../../../profile/home.md). 如果沒有Real-Time CDP B2B Edition，您仍可使用Marketo來源，將人員和活動資料集的資料匯入即時客戶個人檔案以進行分段。

本檔案提供 [!DNL Marketo Engage] 來源聯結器，包括有關如何驗證聯結器、如何對應的資訊 [!DNL Marketo Engage] Experience Data Model (XDM)的欄位以及聯結器的資料延遲。

## 設定Adobe組織對應

建立對應集之前 [!DNL Marketo Engage]，您必須先設定Adobe組織對應。 如需如何完成此工作的詳細步驟，請參閱以下指南中的 [設定Adobe組織對應 [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## 驗證您的 [!DNL Marketo Engage] 聯結器

為了連線 [!DNL Marketo Engage] 對於Platform，您必須先擷取 `munchkinId`， `clientId`、和 `clientSecret`.

請參閱以下說明的步驟 [驗證您的Marketo來源聯結器](./marketo-auth.md) 檔案以擷取您的認證。

## 設定B2B名稱空間和結構描述自動產生公用程式

接下來，使用B2B名稱空間和結構描述自動產生公用程式，設定您的Platform開發人員主控台和Postman環境。 這可讓您自動填入B2B名稱空間和結構描述。 如需詳細指示，請參閱以下指南： [設定您的B2B名稱空間和結構描述自動產生公用程式](./marketo-namespaces.md)

## 體驗資料模式 (XDM)

XDM是公開記錄的規格，提供通用結構和定義，可讓您從協力廠商來源擷取資料，用於下游平台服務。

遵守XDM標準可讓資料統一整合至Platform生態系統，讓您更輕鬆地傳送資料及收集資訊。

若要進一步瞭解XDM及其在Platform中的角色，請參閱 [XDM系統概覽](../../../../xdm/home.md).

## 欄位對應來源 [!DNL Marketo Engage] 至XDM

若要建立來源連線，請執行下列步驟： [!DNL Marketo Engage] 和Platform匯入之前，Marketo來源資料欄位必須對應至其適當的目標XDM欄位。

如需以下欄位對應規則的詳細資訊，請參閱以下內容： [!DNL Marketo Engage] 資料集和平台：

* [活動](../mapping/marketo.md#activities)
* [計畫](../mapping/marketo.md#programs)
* [計畫成員資格](../mapping/marketo.md#program-memberships)
* [公司](../mapping/marketo.md#companies)
* [靜態清單](../mapping/marketo.md#static-lists)
* [靜態清單成員資格](../mapping/marketo.md#static-list-memberships)
* [具名帳戶](../mapping/marketo.md#named-accounts)
* [機會](../mapping/marketo.md#opportunities)
* [機會聯絡人角色](../mapping/marketo.md#opportunity-contact-roles)
* [人員](../mapping/marketo.md#persons)

## 預期延遲 [!DNL Marketo Engage] 平台上的資料

下表概述預期帶來的延遲 [!DNL Marketo Engage] 根據內嵌的性質和所要的目的地，將資料匯入Platform：

| 目的地 | 預期延遲 |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 分鐘 |
| 資料湖 | &lt; 60 分鐘 |

>[!NOTE]
>
>上述延遲數字代表95%信賴水準的預期值。 實際延遲時間會有所不同，在極少數情況下可能會超過這些數字達50%。

## 後續步驟和其他資源

下列檔案提供建立的相關詳細資訊 [!DNL Marketo Engage] 來源連線：

* 如需如何連線的詳細資訊， [!DNL Marketo Engage] 資料到Platform，請閱讀上的教學課程 [建立 [!DNL Marketo Engage] ui中的來源連線](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * 如需如何設定方案和擷取自訂活動資料的詳細資訊，請閱讀以下教學課程： [為建立來源連線和資料流 [!DNL Marketo Engage] 自訂活動資料](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
* 如需用於B2B名稱空間和結構描述的基礎設定相關資訊， [!DNL Marketo Engage]，請閱讀以下檔案： [B2B名稱空間和結構描述](./marketo-namespaces.md).
* 有關尋找您的 [!DNL Marketo Engage] munchkin ID並產生您的認證，請閱讀 [[!DNL Marketo Engage] 驗證指南](./marketo-auth.md).
* 適用於下列專案的特定對應規則的相關資訊： [!DNL Marketo Engage] 資料集，請閱讀以下檔案： [[!DNL Marketo Engage] 欄位對應](../mapping/marketo.md).
* 有關的一般資訊 [!DNL Real-Time Customer Data Platform B2B Edition] 及其功能，請閱讀以下檔案： [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
