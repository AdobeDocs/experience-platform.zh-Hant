---
title: Adobe Experience Platform 發行說明 (2022 年 11 月)
description: Adobe Experience Platform 2022 年 11 月版發行說明。
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 58%

---

# Adobe Experience Platform 發行說明

**發行日期： 2022年11月23日**

Adobe Experience Platform 現有功能的更新：

- [資料集合](#data-collection)
- [體驗資料模式 (XDM)](#xdm)
- [來源](#sources)

## 資料集合 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目標。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 用於事件轉送的[!DNL AWS]延伸模組 | 您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)延伸功能將資料傳送至[!DNL Amazon Web Services] ([!DNL AWS])。 如需詳細資訊，請參閱[[!DNL AWS] 擴充功能概觀](../../tags/extensions/server/aws/overview.md)。 |
| 用於事件轉送的[!DNL Google Ads Enhanced Conversions]延伸模組 | 您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)擴充功能，將轉換資料傳送至[!DNL Google Ads]。 如需詳細資訊，請參閱[[!DNL Google Ads Enhanced Conversions] 擴充功能概觀](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)。 |
| 用於事件轉送的[!DNL Microsoft Azure]延伸模組 | 您現在可以使用[事件轉送](../../tags/ui/event-forwarding/overview.md)延伸功能傳送資料給[!DNL Microsoft Azure]。 如需詳細資訊，請參閱[[!DNL Microsoft Azure] 擴充功能概觀](../../tags/extensions/server/azure/overview.md)。 |

如需Experience Platform資料收集功能的詳細資訊，請參閱[資料收集概觀](../../collection/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 直接新增到結構描述時，將欄位指派給自訂類別 | 當[將個別欄位直接新增到結構描述](../../xdm/ui/resources/schemas.md#add-individual-fields)時，以前您只能將欄位指派給欄位群組作為其父資源。 除了欄位群組之外，您現在可以[將欄位指派給自訂類別](../../xdm/ui/resources/schemas.md#add-to-class)，做為它的父資源。 |

{style="table-layout:auto"}

如需Experience Platform中XDM的詳細資訊，請參閱[XDM系統總覽](../../xdm/home.md)。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Experience Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**更新的功能**

| 功能 | 說明 |
| --- | --- | 
| Oracle服務雲端來源的Beta可用性 | 使用Oracle Service Cloud來源將資料從您的Oracle Service Cloud帳戶擷取至Experience Platform。 如需詳細資訊，請閱讀[Oracle服務雲端來源](../../sources/connectors/customer-success/oracle-service-cloud.md)的檔案。 |

若要深入了解來源，請閱讀[來源概觀](../../sources/home.md)。
