---
title: Adobe Experience Platform 發行說明 (2022 年 11 月)
description: Adobe Experience Platform 2022 年 11 月版發行說明。
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 62%

---

# Adobe Experience Platform 發行說明

**發行日期： 2022年11月23日**

Adobe Experience Platform 現有功能的更新：

- [資料集合](#data-collection)
- [體驗資料模式 (XDM)](#xdm)
- [來源](#sources)

## 資料集合 {#data-collection}

Adobe Experience Platform 提供了一套技術，可讓您收集用戶端的客戶體驗資料，並將其傳送到 Adobe Experience Platform Edge Network，然後在其中擴充及轉換資料，再分送至 Adobe 或非 Adobe 目標。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 用於事件轉送的[!DNL AWS]延伸模組 | 您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)延伸功能將資料傳送至[!DNL Amazon Web Services] ([!DNL AWS])。 如需詳細資訊，請參閱[[!DNL AWS] 擴充功能概觀](../../tags/extensions/server/aws/overview.md)。 |
| 用於事件轉送的[!DNL Google Ads Enhanced Conversions]延伸模組 | 您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)擴充功能，將轉換資料傳送至[!DNL Google Ads]。 如需詳細資訊，請參閱[[!DNL Google Ads Enhanced Conversions] 擴充功能概觀](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)。 |
| 用於事件轉送的[!DNL Microsoft Azure]延伸模組 | 您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)延伸功能傳送資料給[!DNL Microsoft Azure]。 如需詳細資訊，請參閱[[!DNL Microsoft Azure] 擴充功能概觀](../../tags/extensions/server/azure/overview.md)。 |

如需Experience Platform資料收集功能的詳細資訊，請參閱[資料收集概觀](../../collection/home.md)。

## 體驗資料模型 (XDM，Experience Data Model) {#xdm}

XDM 是一種開放原始碼的規格，可為帶入 Adobe Experience Platform 的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併為單一常用表述，以更快速、更整合的方式提供分析洞察。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 直接新增到結構描述時，將欄位指派給自訂類別 | 當[將個別欄位直接新增到結構描述](../../xdm/ui/resources/schemas.md#add-individual-fields)時，以前您只能將欄位指派給欄位群組作為其父資源。 除了欄位群組之外，您現在可以[將欄位指派給自訂類別](../../xdm/ui/resources/schemas.md#add-to-class)，做為它的父資源。 |

{style="table-layout:auto"}

如需有關 Experience Platform 中 XDM 的詳細資訊，請參閱 [XDM 系統概觀](../../xdm/home.md)。
