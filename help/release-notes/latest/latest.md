---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform的最新發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f8e8ec0fb13fc988d47bb3bbe85f953e66b33f13
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 7%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 11 月 23 日**

Adobe Experience Platform 現有功能更新：

- [資料收集](#data-collection)
- [Experience Data Model(XDM)](#xdm)
- [來源](#sources)

## 資料收集 {#data-collection}

Adobe Experience Platform提供一套技術，可讓您收集用戶端客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在中加以擴充、轉換及分發至Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL AWS] 事件轉送擴充功能 | 您現在可以將資料傳送至 [!DNL Amazon Web Services] ([!DNL AWS])使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 擴充功能。 請參閱 [[!DNL AWS] 擴充功能概觀](../../tags/extensions/server/aws/overview.md) 以取得更多資訊。 |
| [!DNL Google Ads Enhanced Conversions] 事件轉送擴充功能 | 您現在可以將轉換資料傳送至 [!DNL Google Ads] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 擴充功能。 請參閱 [[!DNL Google Ads Enhanced Conversions] 擴充功能概觀](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 以取得更多資訊。 |
| [!DNL Microsoft Azure] 事件轉送擴充功能 | 您現在可以將資料傳送至 [!DNL Microsoft Azure] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 擴充功能。 請參閱 [[!DNL Microsoft Azure] 擴充功能概觀](../../tags/extensions/server/azure/overview.md) 以取得更多資訊。 |

如需Platform資料收集功能的詳細資訊，請參閱 [資料匯集概述](../../collection/home.md).

## Experience Data Model(XDM) {#xdm}

XDM是開放原始碼規格，可針對匯入Adobe Experience Platform的資料提供通用結構和定義（結構）。 遵循XDM標準，所有客戶體驗資料皆可整合至通用表示法，以更快速、更整合的方式提供深入分析。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 將欄位直接添加到架構時，將欄位分配給自定義類 | 當 [將個別欄位直接新增至架構](../../xdm/ui/resources/schemas.md#add-individual-fields)，之前您只能將欄位指派給欄位群組作為其父資源。 現在，除了欄位群組，您可以 [將欄位指派給自訂類別](../../xdm/ui/resources/schemas.md#add-to-class) 作為其父資源。 |

{style=&quot;table-layout:auto&quot;}

如需Platform中XDM的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**更新功能**

| 功能 | 說明 |
| --- | --- | 
| oracle服務雲源的測試版可用性 | 使用Oracle服務雲端來源，將資料從您的Oracle服務雲端帳戶內嵌至Experience Platform。 如需詳細資訊，請參閱 [Oracle服務雲端來源](../../sources/connectors/customer-success/oracle-service-cloud.md). |

若要進一步了解來源，請閱讀 [來源概觀](../../sources/home.md).