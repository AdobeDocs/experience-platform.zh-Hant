---
keywords: Experience Platform；首頁；熱門主題；Marketo Engage；marketo engage；marketo
solution: Experience Platform
title: Marketo Engage聯結器
description: 本檔案提供Marketo Engage來源聯結器的概觀，包括其驗證、對應和資料延遲的相關資訊。
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# [!DNL Marketo Engage]聯結器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

[[!DNL Marketo Engage]](https://www.marketo.com/software/)是銷售機會管理的完整解決方案，也適合B2B行銷人員使用，而透過該解決方案，他們可參與複雜購買歷程的每個階段，從中轉變客戶體驗。

透過[!DNL Marketo Engage]來源聯結器，您可以將B2B資料從[!DNL Marketo Engage]帶到Platform，並使用平台連線的應用程式保持這些資料在最新狀態。

>[!IMPORTANT]
>
>您必須有權存取[Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md)，才能將所有Marketo資料集與[即時客戶個人檔案](../../../../profile/home.md)一起用於區段。 如果沒有Real-Time CDP B2B Edition，您仍可使用Marketo來源，將人員和活動資料集的資料匯入即時客戶個人檔案以進行分段。

本檔案提供[!DNL Marketo Engage]來源聯結器的概觀，包括有關如何驗證聯結器、如何將[!DNL Marketo Engage]欄位對應到體驗資料模型(XDM)以及聯結器的資料延遲的資訊。

## 設定Adobe組織對應

您必須先設定Adobe組織對應，才能為[!DNL Marketo Engage]建立對應集。 如需有關如何完成此作業的詳細步驟，請參閱[為 [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html)設定Adobe組織對應的指南。

## 驗證您的[!DNL Marketo Engage]聯結器

為了將[!DNL Marketo Engage]連線到Platform，您必須先擷取`munchkinId`、`clientId`和`clientSecret`的值。

請參閱[驗證您的Marketo來源聯結器](./marketo-auth.md)檔案中概述的步驟，以擷取您的認證。

## 設定B2B名稱空間和結構描述自動產生公用程式

接下來，使用B2B名稱空間和結構描述自動產生公用程式，設定您的Platform開發人員主控台和Postman環境。 這可讓您自動填入B2B名稱空間和結構描述。 如需詳細指示，請參閱[設定B2B名稱空間和結構描述自動產生公用程式的指南](./marketo-namespaces.md)

## 體驗資料模式 (XDM)

XDM是公開記錄的規格，提供通用結構和定義，可讓您從協力廠商來源擷取資料，用於下游平台服務。

遵守XDM標準可讓資料統一整合至Platform生態系統，讓您更輕鬆地傳送資料及收集資訊。

若要進一步瞭解XDM及其在Platform中的角色，請參閱[XDM系統總覽](../../../../xdm/home.md)。

## 從[!DNL Marketo Engage]到XDM的欄位對應

若要在[!DNL Marketo Engage]和Platform之間建立來源連線，Marketo來源資料欄位必須先對應到適當的目標XDM欄位，才能擷取到Platform。

請參閱下列內容，以取得有關[!DNL Marketo Engage]資料集與Platform之間的欄位對應規則的詳細資訊：

* [活動](../mapping/marketo.md#activities)
* [方案](../mapping/marketo.md#programs)
* [計畫成員資格](../mapping/marketo.md#program-memberships)
* [公司](../mapping/marketo.md#companies)
* [靜態清單](../mapping/marketo.md#static-lists)
* [靜態清單成員資格](../mapping/marketo.md#static-list-memberships)
* [具名帳戶](../mapping/marketo.md#named-accounts)
* [機會](../mapping/marketo.md#opportunities)
* [機會聯絡人角色](../mapping/marketo.md#opportunity-contact-roles)
* [人員](../mapping/marketo.md#persons)

## Platform上預期的[!DNL Marketo Engage]資料延遲

下表根據擷取的性質和所要的目的地，概述將[!DNL Marketo Engage]資料帶入Platform的預期延遲：

| 目的地 | 預期延遲 |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10分鐘 |
| 資料湖 | &lt; 60分鐘 |

>[!NOTE]
>
>上述延遲數字代表95%信賴水準的預期值。 實際延遲時間會有所不同，在極少數情況下可能會超過這些數字達50%。

## 後續步驟和其他資源

下列檔案提供有關建立[!DNL Marketo Engage]來源連線的進一步資訊：

* 如需有關如何將您的[!DNL Marketo Engage]資料連線到Platform的資訊，請閱讀有關[在UI](../../../tutorials/ui/create/adobe-applications/marketo.md)中建立 [!DNL Marketo Engage] 來源連線的教學課程。
   * 如需如何設定結構描述和內嵌自訂活動資料的詳細資訊，請閱讀有關[為 [!DNL Marketo Engage] 自訂活動資料建立來源連線和資料流的教學課程](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
   * 如需有關如何將ECID對應從[!DNL Person]資料集移轉至[!DNL Activity]資料集的資訊，請參閱[ECID對應移轉指南](./migration.md)。
* 如需搭配[!DNL Marketo Engage]使用B2B名稱空間和結構描述的基礎設定資訊，請閱讀[B2B名稱空間和結構描述](./marketo-namespaces.md)的檔案。
* 如需尋找您的[!DNL Marketo Engage] munchkin ID及產生認證的相關資訊，請閱讀[[!DNL Marketo Engage] 驗證指南](./marketo-auth.md)。
* 如需有關套用至[!DNL Marketo Engage]資料集的特定對應規則的資訊，請閱讀[[!DNL Marketo Engage] 欄位對應](../mapping/marketo.md)的檔案。
* 如需[!DNL Real-Time Customer Data Platform B2B Edition]及其功能的一般資訊，請閱讀[[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md)的檔案。
