---
title: Adobe Experience Platform發行說明2022年11月
description: 2022年11月為Adobe Experience Platform發佈的說明。
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: ccfc46714069e8c29f1777dea5ba73e318c0a4a6
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 11 月 23 日**

Adobe Experience Platform 現有功能更新：

- [資料收集](#data-collection)
- [體驗資料模型(XDM)](#xdm)
- [來源](#sources)

## 資料收集 {#data-collection}

Adobe Experience Platform公司提供了一套技術，使您能夠收集客戶端客戶體驗資料並將其發送到Adobe Experience Platform邊緣網路，在該網路中，資料可以得到豐富、轉換並分發到Adobe或非Adobe目的地。

**新增或更新的功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL AWS] 事件轉發擴展 | 您現在可以將資料發送到 [!DNL Amazon Web Services] ([!DNL AWS])使用 [事件轉發](../../tags/ui/event-forwarding/overview.md) 擴展。 查看 [[!DNL AWS] 擴展概述](../../tags/extensions/server/aws/overview.md) 的子菜單。 |
| [!DNL Google Ads Enhanced Conversions] 事件轉發擴展 | 您現在可以將轉換資料發送到 [!DNL Google Ads] 使用 [事件轉發](../../tags/ui/event-forwarding/overview.md) 擴展。 查看 [[!DNL Google Ads Enhanced Conversions] 擴展概述](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 的子菜單。 |
| [!DNL Microsoft Azure] 事件轉發擴展 | 您現在可以將資料發送到 [!DNL Microsoft Azure] 使用 [事件轉發](../../tags/ui/event-forwarding/overview.md) 擴展。 查看 [[!DNL Microsoft Azure] 擴展概述](../../tags/extensions/server/azure/overview.md) 的子菜單。 |

有關平台資料收集功能的詳細資訊，請參見 [資料收集概述](../../collection/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新增或更新的功能**

| 功能 | 說明 |
| --- | --- |
| 將欄位直接添加到架構時分配給自定義類 | 當 [將單個欄位直接添加到架構](../../xdm/ui/resources/schemas.md#add-individual-fields)，以前只能將欄位分配給欄位組作為其父資源。 現在，除了欄位組外，您 [將欄位分配給自定義類](../../xdm/ui/resources/schemas.md#add-to-class) 作為其父資源。 |

{style="table-layout:auto"}

有關平台中XDM的詳細資訊，請參見 [XDM系統概述](../../xdm/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**已更新功能**

| 功能 | 說明 |
| --- | --- | 
| oracle服務雲源的Beta可用性 | 使用Oracle服務雲源將資料從Oracle服務雲帳戶接收到Experience Platform。 有關詳細資訊，請閱讀 [Oracle服務雲源](../../sources/connectors/customer-success/oracle-service-cloud.md)。 |

要瞭解有關源的詳細資訊，請閱讀 [源概述](../../sources/home.md)。
