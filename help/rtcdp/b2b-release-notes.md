---
product: adobe experience platform
solution: Experience Platform, Real-time Customer Data Platform
title: Adobe Experience Platform Real-time Customer Data Platform B2B版發行說明
description: Adobe Experience Platform Real-time Customer Data Platform B2B版的最新發行說明。
source-git-commit: 4417670d167d7390d0e82ac5c32a1a6b46a15226
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---

# Adobe Experience Platform Real-time Customer Data Platform B2B版發行說明

**發行日期：2021 年 11 月 12 日**

## Real-time Customer Data Platform更新

Real-time CDP B2B Edition建置在Real-time Customer Data Platform(Real-time CDP)之上，專為以企業對企業服務模式運作的行銷人員而打造。 它匯集了來自多個來源的資料，並將其結合為人員和帳戶設定檔的單一檢視。 此統一的資料可讓行銷人員精確鎖定特定對象，並參與所有可用管道中的這些對象。

對各種Adobe Experience Platform功能進行了改進，將即時CDP B2B Edition與其B2C對應版本區分開來。 其中包括針對B2B使用案例改善Experience Data Model(XDM)、升級為身分解析和設定檔分段，以及自訂的連接器和Marketo Engage目的地。 Marketo連接器可讓B2B品牌將其業界領先的B2B參與資料與行為資訊連結，以培育銷售機會並增強以帳戶為基礎的行銷作業。

-[**全新B2B和B2P版本**](#editions)
-[**全新Marketo資料來源和目的地連接器**](#marketo)
-[**標準B2B XDM**](#XDM)

## 全新B2B和B2P版本 {#editions}

**全新B2B和B2P版本** 可購買將ABM資料和功能整合至即時CDP和Platform Activation產品的ABM。

要了解有關Real-time CDP B2B Edition的更多資訊，請參見 [概述](./b2b-overview.md)

## 全新Marketo資料來源和目的地連接器 {#marketo}

**全新Marketo資料來源和目的地連接器** 將Marketo資料串流至Platform和Platform閱聽眾，並傳回Marketo。 適用於所有平台使用者。

| 功能 | 說明 |
|---|---|
| Marketo Engage源連接器 | Marketo Engage來源連接器可讓行銷人員將其一或多個Marketo執行個體的資料流暢內嵌至其Adobe Experience Platform執行個體，並為銷售機會管理和B2B行銷人員提供完整的解決方案。 |
| Marketo Engage目標 | 此 [Marketo目的地](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html) 可讓行銷人員將在Adobe Experience Platform中建立的區段推送至Marketo，這些區段會顯示為靜態清單。 |

若要深入了解Marketo Source Connector，請參閱 [概述](../sources/connectors/adobe-applications/marketo/marketo.md)

## 標準B2B XDM {#XDM}

**標準B2B XDM** 所有Platform使用者皆可使用類別、欄位群組和資料類型。

| 功能 | 說明 |
|---|---|
| 標準B2B XDM類別 | Real-time Customer Data Platform B2B版提供數種標準XDM，可擷取關於基本B2B資料實體（例如帳戶、機會、行銷活動等）的詳細資訊 |

請參閱 [Real-time Customer Data Platform B2B版中的結構描述](./schemas/b2b.md) 以進一步了解擷取B2B資料實體。
